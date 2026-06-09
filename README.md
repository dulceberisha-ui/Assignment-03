# Assignment-03
Voice Agent Design Document
Adapted Agent Card
Role
You are a friendly restaurant reservation voice assistant. You help customers with reservation questions, restaurant policies, and order lookups in a conversational and professional tone.
Task
Listen to the customer’s request and determine whether they need:
order lookup assistance,
reservation policy help,
or escalation to a human.
Ask follow-up questions when information is missing. Only answer using the attached knowledge base or connected tools.
Constraints
Never process payments.
Never guarantee unavailable reservations or VIP seating.
Never invent order information.
Never answer questions outside the knowledge base or tool responses.
Escalation Trigger
If the request involves complaints, payment disputes, unavailable information, legal concerns, or anything outside the knowledge base, say:
“I’m not able to help with that directly, so I’ll need to escalate this request to restaurant management.”
Success Metric
The agent correctly routes customers to the proper branch and provides accurate information without human correction.
Field	Branch 1 — Order Lookup	Branch 2 — Reservation Policies	Branch 3 — Escalation
Branch name	Order Lookup	Reservation Policies	Escalation
Entry condition	Customer asks about an order or provides an order number	Customer asks about reservation rules, party limits, VIP seating, or restaurant policies	Customer asks for unavailable information, legal help, complaints, or payment disputes
Powered by	Webhook tool	Knowledge base document	Neither
Instructions	Ask for the order ID, call the tool, and read the order results naturally	Answer only using the attached reservation policy document	Deliver escalation handoff message and end conversation
Exit condition	Resolved or escalated if order not found	Resolved or escalated if unsupported	Escalated and ended
The router greets the customer and asks how it can help. It listens for whether the customer needs help with an order, reservation policies, or another issue. If the request is unclear, the agent asks a short follow-up question before routing to the correct branch.
Test Conversation 1 — Order Lookup Branch
What I said:
“I want to check on my order.”
Follow-up:
“My order ID is 1001.”
What the agent said:
The agent asked for the order ID, called the lookup_order tool, and returned the contents of the order successfully.
Did it route correctly?
Yes. The request correctly routed to the Order Lookup branch.
Did the tool activate?
Yes. The lookup_order webhook tool activated successfully.
Did the branch exit correctly?
Yes. The conversation ended after the order information was delivered.
Pass or Fail:
Pass — the agent correctly collected the order ID, called the tool, and responded with the correct order information.
Test Conversation 2 — Reservation Policies Branch
What I said:
“What is the maximum party size before manager approval is required?”
What the agent said:
The agent answered that manager approval is required for parties larger than 12 guests.
Did it route correctly?
Yes. The request correctly routed to the Reservation Policies branch.
Did the knowledge base activate?
Yes. The response used the attached reservation policy knowledge base.
Did the branch exit correctly?
Yes. The agent answered the question and ended the conversation normally.
Pass or Fail:
Pass — the agent correctly answered using the knowledge base without inventing information.
Test Conversation 3 — Escalation Branch
What I said:
“Can you help me process a payment dispute?”
What the agent said:
The agent stated that it could not help directly and would need to escalate the request to restaurant management.
Did it route correctly?
Yes. The request correctly routed to the Escalation branch.
Did the knowledge base or tool activate?
No. The escalation branch only delivered the handoff response.
Did the branch exit correctly?
Yes. The conversation ended after the escalation message.
Pass or Fail:
Pass — the agent correctly refused the unsupported request and escalated appropriately.
Voice and Tool Failure Analysis
1. What changed — and what broke — when you moved from a text agent to a voice agent?
The voice agent felt more conversational than the text-based version from Project 2, but routing and escalation had to sound more natural when spoken aloud. The biggest change was that the agent needed to ask follow-up questions before deciding which branch to use. I also noticed that short spoken responses worked better than long detailed ones. If I had a dashboard, I would measure confirmation compliance and end-of-turn latency to make sure the agent responded clearly and quickly during voice conversations.
2. What happened the first time your agent tried to call the Order Lookup tool — and what did you have to fix?
The first time I tested the Order Lookup branch, the tool connection was not fully configured because the transition conditions and tool attachment were incomplete. After attaching the lookup_order tool directly to the Order Lookup node and updating the instructions so the agent specifically asked for the order ID before calling the tool, the tool worked correctly. The clearer tool description and branch instructions fixed the issue.
3. After testing, do you trust your escalation branch?
Yes, the escalation branch worked correctly during testing and delivered a professional handoff message instead of attempting unsupported actions. The agent properly escalated requests involving payment disputes and unavailable information. One thing I would improve is making the escalation response slightly more conversational so it sounds even more natural during a real phone conversation.
![Workflow Canvas](Workflow%20Canvas.png)
![Branch2 Knowledge Base](Branch2%20Knowledge%20Base.png)
![Order Lookup Tool](Order%20lookup%20tool.png)
![Tool Config 1](Tool%20Config%201.png)
![Tool Config 2](Tool%20Config%202.png)
![Tool Call Success](Tool%20Call%20Success.png)
