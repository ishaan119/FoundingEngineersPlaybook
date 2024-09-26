# Founding Engineer's Playbook

# Table of Contents

1. [Introduction](#-introduction)
2. [Code Review](#-code-review)
3. [Git Hooks](#-git-hooks)
4. [Code Release Management](#-code-release-management)
5. [CI/CD](#-code-release-management)
6. [Monitoring and Error Tracking](#-monitoring-and-error-tracking)
7. [Security Best Practices](#-security)

## 🚀 Introduction

The idea behind this book is personal and something I felt would have helped me when I first become the first engineer of a startup. In my experience even lot of startups with good traction and seed funding would benefit a lot from this. 

This is not a comprehensive list of to do things, but just enough to get you started. The whole idea of this book is understand how to ship things faster and with good quality. 

## 📝 Code Review

_Boy Scout Rule: Leave the code better than you found it._



> [!NOTE]
>  - Agree on style guides and **automate** them.
>  - Set a clear process for reviewers and PR structure.
>  - Keep PRs **small** (<200 lines).
>  - PRs shouldn’t sit open for days—respond **fast**.
>  -  Document important decisions (not in PR comments).
>  -  Stay humble —focus on merging, not ownership. 


Code reviews typically become necessary when teams grow, and physiologically I have always found the code quality is better when you know someone is going to look at your code. If you're a couple of senior engineers, you might not need formal code reviews, but it’s still good to establish the process early.

If you are the only engineer on the team, skip this, but be aware that some form of review adds a lot of value. Reviews can be in the form of Pair programming, automated testing etc.

> Opinion: It’s hard to hire senior engineers at early-stage startups, and most of the time, you end up with junior devs. Code reviews or pair programming are a great way to help them improve. 

Reviews aren’t just for catching bugs—they're great for sharing best practices and experiences across the team. Plus, it’s **10x cheaper** to catch bugs early instead of in production.

But beware: Code reviews can also highlight poor culture and unprofessional behavior. Without proper management, they can slow things down or hurt morale.

Also, being a good developer doesn’t make you a good reviewer. Great reviewers know how to:
- Give constructive feedback.
- Respond to comments.
- Know what to ignore and where to push.

#### Setting Up Code Reviews

Before you start, agree on some fundamentals and automate where you can.

1. **Style guides**: Every language has them, and they save time. Don’t waste time debating styling in reviews—it takes the focus away from catching bugs. Agree on a style guide and automate it.

2. **Process**: Define who reviews the code and how many reviewers are needed. Usually reviewers who has written the original code or who has business context is ideal.

3. **PR size and timelines**: Set rules for PR size (e.g., under 200 lines) and how long a PR can stay open (less than 24 hours).

4. **PR format**: Define the structure of commit messages, including using identifiers (like bug IDs).

5. **Document decisions**: Don’t let key decisions live in PR comments—no one checks those later. Update the design doc or the code itself if something important is decided.

6. **Right attitude**: Don’t just critique; give sincere praise too. It boosts morale. And always review PRs promptly. If a developer updates their code based on feedback, acknowledge it and move forward.

7. **Atomic commits**: Keep changes small and logical. Don’t try to fix everything in one PR.

8. **Disagreements**: Set up an escalation path when disagreements arise (they will!). Resolve conflicts quickly to avoid hurting team velocity and morale. Make a decision and move on—don’t let things linger.


## 🔧 Git Hooks


_Automation doesn’t just catch mistakes—it eliminates the awkwardness of a human having to point them out._


>  [!NOTE]
> - The ultimate sidekick that automates the boring stuff, catches mistakes, and boosts your ROI—like having a code ninja that never sleeps!

Git hooks are so awesome that they deserve a dedicated chapter! Adding Git hooks early on in your project is probably the best ROI you'll get. There are numerous pre-written Git hooks that you can quickly integrate into your workflow.

#### Popular Git Hooks:
- **Linting**: Enforce coding standards across your team.
- **File checks**: Ensure no unnecessary files are being committed.
- **Commit message formatting**: Enforce consistency in commit messages.
- **Static analysis**: Catch bugs and errors before they enter your codebase.

The beauty of Git hooks is their flexibility. As long as the hook script is executable, Git doesn’t care which language it’s written in—whether it’s Bash, Python, or anything else.

Even if you’re working with an existing project, you can start using Git hooks immediately without affecting any of the current code. It's a seamless addition to your workflow, and I highly recommend starting as early as possible.

#### A Word of Caution
Git hooks are primarily designed to enhance developer productivity and encourage defensive programming practices. However, keep in mind that developers can disable these hooks if they choose to (hopefully they won’t!). Additionally, running these hooks on GitHub requires a paid service.

#### Examples of Git Hooks:
- **pre-commit**: Check the commit message for spelling errors.
- **pre-receive**: Enforce coding standards before a commit is accepted.
- **post-commit**: Automatically send an email or SMS to team members notifying them of a new commit.
- **post-receive**: Push the code to production after a commit is received.

The possibilities for Git hooks are only limited by the developer’s imagination. They can be customized to fit any part of your workflow, enhancing automation and consistency throughout the development process.

For a collection of useful Git hooks, check out [githooks.com](https://githooks.com/).


## 📦 Code Release Management


_The balancing act between order and chaos—because no process is perfect, but skipping one guarantees chaos!_


> [!NOTE]
> Startups often struggle with overly complex or too basic release processes, so it's essential to pick the right workflow.
>
> - Trunk-Based Development: Great for fast-moving teams; always production-ready, but requires 
   strong CI/CD and senior engineers.
> - Git Flow: Best for legacy or structured environments; multiple branches for control, but has a 
   learning curve and longer path to production.
> - Feature Branching: A hybrid of both, enabling concurrent feature development, but can inherit 
  downsides from both approaches.

This is something I have seen most of the startups struggle with. Either you have super complicated process following what you did at an established company or something very basic which will eventually create a mess. 

The goal of this chapter is to familiarize you with different code release workflows. I wanted to familiarize you with different options and you then you can take a call. Understanding different flows and their pros/cons will help you advocate for the best one for your team.

We'll assume you're using Git—if not, you'd better have a solid reason.

### Trunk-Based Development

**Trunk-Based Development** is one of the most popular workflows for fast-moving teams.

> Opinion: If you're starting fresh without legacy baggage, I highly recommend using this flow.

#### Key Features:
- Single branch (`main`/`master`)
- Commit directly to `main`, using very short-lived branches (less than 24 hours)
- `main` is always production-ready and deployed after every commit

For this to work, you need a solid CI/CD pipeline with comprehensive unit and integration testing. **Feature flags** are also essential for scalability.
This is a developer's dream for a fast-moving team, but there are some trade-offs.
This workflow is ideal for smaller teams (<10 engineers) with a strong CI/CD system. If you have compliance needs or a QA team that doesn't release frequently, this might not be the best fit.


### Git Flow


Git Flow** is one of the most well-known workflows in the industry.

- Suited for teams with fixed release cycles
- Multiple long-living branches, typically `main` (or `master`) and `develop`
- Additional branches for features, releases, and hotfixes

> Opinion: In practice, using three long-living branches (`main`, `qa`, `develop`) makes development smoother.If you’re dealing with legacy software, Git Flow is often the best option.


This workflow excels in environments with specific testing, compliance needs, and larger teams. It provides clear traceability for features, testing status, and live releases.

#### Example Workflow:
- Developers merge code into `develop`.
- QA merges `develop` into `qa` for testing.
- Once `qa` is stable, it’s merged into `main` for release.
- Hotfixes are directly merged into `main`, but also need to be applied to `develop` and `qa` for consistency.

If you don’t need a QA branch, you can create a short-lived release branch from `develop` when necessary.

This flow is great for staggered production releases, accountability, and traceability. Just be sure to protect branches and clean up old ones.

### Feature Branching

**Feature Branching** aims to combine the best of Trunk-Based Development and Git Flow.

- Single long-lived `main` branch
- Short-lived feature branches for concurrent development
- `main` is always production-ready, thanks to a strong CI/CD pipeline


> Opinion: I’m not a fan of this hybrid approach—it takes on the negatives of both Trunk-Based and Git Flow without enough benefits.

| Release Management Workflow | Pros                                                                 | Cons                                                                                                  |
|-----------------------------|---------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------|
| **Trunk-Based Development**  | - Simple workflow<br>- Codebase is always production-ready<br>- Fewer merge conflicts<br>- Matches the latest commit | - Requires a robust CI/CD setup<br>- Relies on senior engineers<br>- Feature flag clutter<br>- Limited traceability |
| **Git Flow**                 | - Well-suited for staged releases<br>- Great for legacy systems<br>- Provides traceability and accountability | - Complex and requires DevOps management<br>- Common merge conflicts<br>- Longer path to production<br>- Steeper learning curve |
| **Feature Branching**        | - Allows concurrent feature development<br>- Isolates feature work<br>- Reduces risk in main branch<br>- Better control over feature releases | - Merge conflicts can still happen<br>- Inherits complexity from both Git Flow and Trunk-Based Development<br>- Can slow down production readiness |



_The most important thing is to pick a workflow that fits your team and implement it properly. The worst-case scenario is having no workflow, leading to ad-hoc releases with no visibility or accountability._

Once you've chosen a flow, make sure there are clear checks and balances to prevent bypassing the process.


## 🛠️ CI (Continuous Integration)/CD (Continuous Deployment) 

_Where the art of pushing buttons turns into the science of keeping your app from going up in flames!_


> [!NOTE]
> Set up your CI/CD early—it's easier when you're starting out and saves headaches later.
> Start simple with managed services like Heroku or Elastic Beanstalk—let them handle DevOps so you can focus on building.
> Avoid microservices early on—you’ll likely need to rebuild anyway as you scale, so don’t slow yourself down by over-optimizing too soon.

CI/CD is one of the most useful yet misunderstood terms in the industry. It’s important to note that **Continuous Integration (CI)** and **Continuous Delivery/Deployment (CD)** are two distinct concepts, and you can have one without the other.

- **Continuous Integration (CI)**: Automates the process of merging code from multiple developers, running tests, and building the project.
- **Continuous Delivery/Deployment (CD)**: Focuses on automating deployments to production and other environments.

There are many tools available to support CI/CD, and I highly recommend setting them up early. It’s easier to implement when you’re starting out, and it becomes progressively harder the later you leave it.

If you’re using GitHub, I recommend **GitHub Actions**. It’s a powerful tool with excellent community support via the marketplace.

> Opinion: I guarantee that if you are deploying your code manually you will end up spending more time than the time it takes to setup CD.

#### A Note on Microservices

As an early-stage founder, **do not start with microservices**, even if you anticipate needing them in the future. Most frameworks are designed to allow you to separate components later, if necessary. 

In my experience, as you scale, you’ll likely need to **rebuild your product** anyway. The decisions you make at 1,000 users will not hold at 50,000 or 500,000 users. Over-optimizing for scale too early will only slow down your feature development.

> Opinion: All major cloud providers offer managed services like **Elastic Beanstalk** or **Heroku**. These services handle a lot of the DevOps overhead for you, so you can focus on building your product. Since they are containerized, you can migrate to **Kubernetes** or your own clusters later if needed.

#### Starting Simple

Start with a **monolith** on managed services like Heroku, Elastic Beanstalk, or Vercel. Also, use managed databases. While they might be more expensive, it’s worth the peace of mind not having to worry about losing data. 

> Pro Tip: Use an auth provider like **Auth0**, **Clerk**, or **Firebase** so you don’t have to manage authentication yourself.

#### Early Stage Focus

In the early stages, your goal should be to move fast, deploy features, and find product-market fit. Keep in mind that these decisions will incur **technical debt**, and you’ll likely need to refactor later. But that’s a good problem to have!


## 📊 Monitoring and Error Tracking

_Because relying on your resident superhero to fix everything might make for great stories, but it’s a terrible strategy for your team’s sanity!_

> [!NOTE]
> Error tracking and performance monitoring are often overlooked in startups, leading to one overburdened "maverick" constantly firefighting. Avoid this by using tools like Sentry and Loggly to make logs and error reports accessible to the entire team without needing production access. Focus on being proactive with monitoring to boost productivity and avoid burnout. Let your team fix issues before they become emergencies.

Error tracking and performance monitoring are often afterthoughts in early-stage companies. Since engineers frequently interact with customers directly, they tend to fix issues as they arise or when users report them.

What typically happens is that one highly skilled engineer—who understands the codebase well—ends up being bombarded with user queries and issues, drastically reducing their productive time. Every startup has that one "maverick" who ends up fixing everything.

While this **maverick (firefighting) culture** is common in startups, it’s extremely counterproductive. The right approach is usually to **fix the issue properly** or let the team handle it without one person constantly jumping in.

This culture arises because there is often **no proper error logging or monitoring**, and only a few people have production access. Even if other team members could fix the issue, the maverick ends up diving in to "save the day." It makes for great stories but results in a terrible developer experience.

#### Fixing the Problem

With the tools available today, solving this issue is straightforward. Pick any central logging tool like **Loggly**, **Papertrail**, or even cloud provider-based logging systems. What’s important is ensuring that the **team** can see production logs without needing direct access to the production servers.

Additionally, use tools like **Sentry**, which can alert the team when an exception occurs. Most frameworks also have built-in error tracking if you prefer not to use third-party tools.

> Opinion: In my teams I have seen the biggest ROI with implementing tools like sentry where crashes are reported (emailed  to the whole team) and a bug is added automatically to your bug tracker. 

I cannot emphasize enough how much time and effort this saves. By implementing proactive monitoring, you improve the developer experience and prevent the team from being caught off guard by issues.

Also use tools like new relic to keep track of your performance and speed. You don't need to make everything super optimized, but its always a to know what tech improvements can be done when the team has some downtime. 

The goal is to be **proactive** rather than **reactive**.

## 🔒 Security

_Security might feel like an afterthought until one wrong click makes it your only thought._

>[!NOTE]
>Don’t neglect security in early-stage startups. Encrypt sensitive data, use SSL, and manage permissions with group-based controls. Update software regularly, secure cloud storage with encryption, and use password managers with SSO for secure access. Leverage tools like WAFs to block malicious traffic and enforce least privilege principles. Starting early prevents major issues later.


Security often takes a back seat in early-stage startups, but it’s one area you can’t afford to ignore. A single breach could sink your company. Fortunately, basic security practices can significantly reduce your risk with minimal effort.

Essential Security Measures
1. Encrypt Sensitive Data
Never store passwords or sensitive data in plaintext. Always hash and encrypt such data before storing it to prevent unauthorized access, especially when many team members have database access.

2. Always Use SSL
Ensure SSL is enabled on all web traffic to protect data in transit. Even though it’s standard practice, it’s still occasionally overlooked.

3. Group-Based Access Control
Implement group-based privileges instead of individual permissions. This simplifies user management, making it easier to add or remove team members without having to adjust individual permissions manually.

4. Regular Software Updates
Schedule regular software updates, ideally every 6 months. Keeping your software up to date ensures you patch vulnerabilities early and avoid the dreaded pile-up of tech debt.

5. Secure Cloud Storage (S3, etc.)
For services like S3, always:

Encrypt files using built-in options like AWS’s Server-Side Encryption (SSE).
Disable public access to storage by default and control access via bucket policies.
Use signed URLs for temporary access and audit permissions regularly to ensure they’re limited to authorized users.
6. Use Password Managers & Single Sign-On (SSO)
Require the use of password managers like 1Password or LastPass to ensure secure, unique passwords for each service. Implement SSO wherever possible to centralize user authentication, making access management simpler and more secure.

7. Web Application Firewall (WAF)
For added protection, use a Web Application Firewall (WAF) to block malicious traffic and common web exploits without much additional setup or maintenance.

8. Principle of Least Privilege
Follow the principle of least privilege by giving users only the access they need. Group-based permissions make this easier to enforce.

9. Secure File Uploads
Ensure uploaded files are stored securely. Misconfigurations often leave sensitive files exposed. Regularly audit file security and permissions to avoid accidental leaks.

