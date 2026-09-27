What is Cloud Computing?

Cloud Computing means using computing resources(on demand of IT services) — servers, storage, databases, networking, software — over the internet ("the cloud") instead of owning and running physical hardware yourself.

Instead of buying a physical server, installing it in your office, and maintaining it, you rent computing power from a provider (like AWS, Azure, or Google Cloud) and pay only for what you use.
Simple Example

Imagine you want to run a website:

Without cloud: You buy a server, set up cooling, power backup, networking, hire staff to maintain it.
With cloud: You click a few buttons on AWS, get a virtual server (EC2 instance) in minutes, and pay only for the hours you use it.

Types of Cloud
1. Public Cloud

This is the most common type — infrastructure (servers, storage, networking) is owned by a third-party provider like AWS, Microsoft Azure, or Google Cloud, and made available to the general public over the internet.

How it works: The provider owns massive data centers around the world. Thousands of different companies share that same physical infrastructure (this is called multi-tenancy) — but logically, everyone's data and resources are isolated and secure from each other.

Why companies use it:

No upfront hardware cost — you don't buy servers
Scales instantly — need more power? Just spin up more instances
Maintenance (hardware failures, patching, cooling, power) is handled by the provider
Pay only for what you consume

Downsides:

You don't have physical control over the hardware
Security/compliance can be a concern for very sensitive data (banking, government)
Ongoing costs can add up if not managed well

Real example: Netflix runs almost entirely on AWS — it doesn't own the servers streaming your shows.

2. Private Cloud

Here, the cloud infrastructure is used by only one organization — it's not shared with anyone else. It can be:

Hosted on the company's own premises (their own data center), or
Hosted by a third party, but dedicated only to that one company (not shared)

Why companies use it:

Full control over hardware, security, and configuration
Better for industries with strict compliance needs (banks, hospitals, government)
Data never leaves the organization's own controlled environment

Downsides:

Expensive — you still need to buy and maintain hardware
Less elastic — scaling up means buying more physical equipment
Requires an in-house IT team

Real example: A large bank might run its core transaction systems on a private cloud to meet strict regulatory requirements.

3. Hybrid Cloud

This combines public + private cloud, connected together so data and applications can move between them.

Why companies use it:

Keep sensitive/critical data on private cloud (for security/compliance)
Use public cloud for scalable workloads (like handling traffic spikes)
Best of both worlds: control + flexibility

Common pattern — "Cloud Bursting":
A company runs its normal workload on a private cloud, but when there's a sudden spike in demand (e.g., Black Friday sale), it automatically "bursts" extra traffic onto the public cloud temporarily.

Real example: A hospital keeps patient records in a private cloud (for HIPAA compliance) but uses AWS's public cloud for running data analytics or hosting its public website.
