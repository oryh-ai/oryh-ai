# What If the ERP User Is an Agent?

*When Agents Start Operating the Business: Design Explorations from ORYH — Article 2*

Once we had a working timesheet service, a question started becoming more concrete. If people used to fill in the forms, and now an agent calls the APIs, how much does the software itself need to change?

At first glance, perhaps not much. An employee says, “Help me submit this week's timesheet.” The agent organizes the data, calls the endpoints, and says it's done. Put a chat interface in front of the existing application, and that seems to cover it.

As we kept building ORYH, though, some fairly ordinary implementation details turned out to matter much more when the caller was an agent.

## Having an API isn't quite enough

One example was a date update. We had an endpoint that didn't accept a date field. If a request included that field anyway, the server quietly ignored it and returned success.

Our own frontend didn't readily expose the problem. Its request fields were fixed in advance. An agent, however, might reasonably try to update the date because that's what the person asked it to do. A successful response could then lead it to report, “I've fixed the date,” even though nothing had changed.

That's an awkward failure. The person isn't watching an application screen refresh. They're relying on the agent's account of what happened. A success response that means “I ignored part of your request” gives the agent very little chance of explaining the situation correctly.

We eventually made request validation stricter. Unsupported fields are rejected, and the response names the field that caused the problem. That doesn't guarantee the agent will know how to recover. At least it won't carry on with a false success.

This was a useful reminder: conventions that used to live inside our frontend don't automatically travel with an API. The interface has to say what it accepts and what it failed to do. We can't leave that for the agent to guess.

## Fewer calls aren't only about speed

Creating a document raised a different issue. The original API split looked quite natural from the database side: create the header, add the lines one at a time, then submit. An ordinary program can do that with a loop.

But our Skills taught the same sequence, so agents followed it turn by turn. A five-day timesheet involved several waits. The endpoints themselves weren't particularly slow. Much of the time went into the agent reading each result and issuing the next call.

We changed creation so the header and its lines could arrive together. Besides reducing round trips, this gave us a better transaction boundary. If one line was invalid, the whole creation rolled back. We no longer had to leave a half-written document behind just because a later line failed.

Submission remained a separate operation, though. We wanted to keep the point where the person reviews the contents and explicitly confirms them. Saving one more call wasn't worth removing that distinction.

Looking back, the unit of the API was shifting. It wasn't always “one write to one table” anymore. It was becoming “one complete action that makes sense for the task.” That takes a little more thought than replacing a button with a chat message.

## So, do we still build screens?

Yes. An administrator needs to inspect permissions. An approver may want to look directly at the lines. When something goes wrong, someone needs a place to examine the records. Handing everyday operations to an agent shouldn't leave a company able to see its own business only through a conversation.

What we stopped assuming was that every new capability needed a new page first, followed by instructions teaching employees how to use it.

Take “who should review this document next?” We'd rather have an agent read the company's workflow definition and work that out than keep adding routing branches to the backend. ORYH stores the document, the rule text, the todos, and the approval facts. Code still handles the hard constraints: line-item arithmetic, permission checks, and preventing a payment from being over-applied.

So the change isn't just about how someone operates the application. Business judgment that would otherwise sit in application code starts moving to the agent. The remaining software is mostly concerned with keeping the records accurate and refusing things that must not happen.

These days, a new requirement prompts an extra question: do we need a page, an API operation, or a clearer statement of the company's rules for the agent to follow?

We don't always get that distinction right. But starting with “what does the agent need to know, and what must the server guarantee?” rather than “what should this page look like?” has already led us to some different designs.
