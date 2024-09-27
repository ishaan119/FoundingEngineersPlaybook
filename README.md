<img width="1069" alt="Screen Shot 2024-09-27 at 12 59 09 PM" src="https://github.com/user-attachments/assets/c2bdf5e3-b406-48ff-b22f-ef6b52d69e9b">

# Founding Engineer's Playbook

This playbook is designed for founding engineers and early technical hires at startups. It provides essential guidance on establishing robust engineering practices, from code reviews to security measures. 

## Key Takeaways

- **Implement code reviews early** to improve code quality and knowledge sharing.
- **Utilize Git hooks** for automated checks and consistency.
- **Choose an appropriate code release management workflow** for your team size and needs.
- **Set up CI/CD pipelines early** to streamline development and deployment.
- **Implement proper monitoring and error tracking** to prevent a "firefighting" culture.
- **Don't neglect basic security measures**, even in the early stages.

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

This is not a comprehensive list of to do things, but just enough to get you started. The main idea is to allow you and your team to be able to push code with confidence and ship faster.Use this playbook as a guide, adapting the recommendations to fit your specific context and needs.

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


| **Aspect**               | **Description**                                                                                                                                                                    |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Style guides**          | Every language has them, and they save time. Don’t waste time debating styling in reviews—it takes the focus away from catching bugs. Agree on a style guide and automate it.      |
| **Process**               | Define who reviews the code and how many reviewers are needed. Usually, reviewers who wrote the original code or who have business context are ideal.                              |
| **PR size and timelines** | Set rules for PR size (e.g., under 200 lines) and how long a PR can stay open (less than 24 hours).                                                                                |
| **PR format**             | Define the structure of commit messages, including using identifiers (like bug IDs).                                                                                               |
| **Document decisions**    | Don’t let key decisions live in PR comments—no one checks those later. Update the design doc or the code itself if something important is decided.                                 |
| **Right attitude**        | Don’t just critique; give sincere praise too. It boosts morale. Always review PRs promptly. If a developer updates their code based on feedback, acknowledge it and move forward.  |
| **Atomic commits**        | Keep changes small and logical. Don’t try to fix everything in one PR.                                                                                                            |
| **Disagreements**         | Set up an escalation path when disagreements arise (they will!). Resolve conflicts quickly to avoid hurting team velocity and morale. Make a decision and move on—don’t linger.    |



## 🔧 Git Hooks


_Automation doesn’t just catch mistakes—it eliminates the awkwardness of a human having to point them out._


>  [!NOTE]
> - The ultimate sidekick that automates the boring stuff, catches mistakes, and boosts your ROI—like having a code ninja that never sleeps!

Git hooks are so awesome that they deserve a dedicated chapter! Adding Git hooks early on in your project is probably the best ROI you'll get. There are numerous pre-written Git hooks that you can quickly integrate into your workflow.

_Some Popular Git Hooks_

| Git Hook                  | Purpose                                                          |
|---------------------------|------------------------------------------------------------------|
| **Linting**                | Enforce coding standards across your team.                       |
| **File Checks**            | Ensure no unnecessary files are being committed.                 |
| **Commit Message Formatting** | Enforce consistency in commit messages.                       |
| **Static Analysis**        | Catch bugs and errors before they enter your codebase.           |


The beauty of Git hooks is their flexibility. As long as the hook script is executable, Git doesn’t care which language it’s written in—whether it’s Bash, Python, or anything else.

Even if you’re working with an existing project, you can start using Git hooks immediately without affecting any of the current code. It's a seamless addition to your workflow, and I highly recommend starting as early as possible.

>[!WARNING]
>Git hooks are primarily designed to enhance developer productivity and encourage defensive programming practices. However, keep in mind that developers can disable these hooks if they choose to (hopefully they won’t!). Additionally, running these hooks on GitHub requires a paid service.

_Different types of Git Hooks_

| Git Hook      | Purpose                                                                                   |
|---------------|--------------------------------------------------------------------------------------------|
| **pre-commit**  | Check the commit message for spelling errors.                                             |
| **pre-receive** | Enforce coding standards before a commit is accepted.                                     |
| **post-commit** | Automatically send an email or SMS to team members notifying them of a new commit.        |
| **post-receive**| Push the code to production after a commit is received.                                   |


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

This is something I have seen most of the startups struggle with. Either you have super complicated process following what you did at an established company or something very basic which will eventually slow down your team. 

The goal of this chapter is to familiarize you with different workflows and then you can take a informed decisions.

We'll assume you're using Git—if not, you'd better have a solid reason.

### Trunk-Based Development

**Trunk-Based Development** is one of the most popular workflows for fast-moving teams.

#### Key Features:
1. Single branch (`main`/`master`)
2. Commit directly to `main`, using very short-lived branches (less than 24 hours)
3. `main` is always production-ready and deployed after every commit

<img width="718" alt="Screen Shot 2024-09-27 at 2 20 50 AM" src="https://github.com/user-attachments/assets/b9eb8825-578e-44e7-95b6-566adc4f2981">


For this to work, you need a solid CI/CD pipeline with comprehensive unit and integration testing. **Feature flags** are also essential for scalability.
This is a developer's dream for a fast-moving team, but there are some trade-offs.
This workflow is ideal for smaller teams (<10 engineers) with a strong CI/CD system. If you have compliance needs or a QA team that doesn't release frequently, this might not be the best fit.

### Git Flow


**Git Flow** is one of the most well-known workflows in the industry.

1. Suited for teams with fixed release cycles
2. Multiple long-living branches, typically `main` (or `master`) and `develop`
3. Additional branches for features, releases, and hotfixes

This workflow excels in environments with specific testing, compliance needs, and larger teams. It provides clear traceability for features, testing status, and live releases.

<img width="1053" alt="Screen Shot 2024-09-27 at 2 24 41 AM" src="https://github.com/user-attachments/assets/bea6321f-30d2-4ab7-bd27-8945582730f8">

This flow is great for staggered production releases, accountability, and traceability. Just be sure to protect branches and clean up old ones.

### Feature Branching

**Feature Branching** aims to combine the best of Trunk-Based Development and Git Flow.

1. Single long-lived `main` branch
2. Short-lived feature branches for concurrent development
3. `main` is always production-ready, thanks to a strong CI/CD pipeline

<img width="767" alt="Screen Shot 2024-09-27 at 2 25 10 AM" src="https://github.com/user-attachments/assets/c60a4e34-8d4b-4637-a6de-6cfe9b2e0797">

### Pro's and Con's

| **Release Management Workflow** | **Pros**                                                                                              | **Cons**                                                                                                                    |
|----------------------------------|------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------|
| **Trunk-Based Development**      | - Simple workflow<br>- Codebase is always production-ready<br>- Fewer merge conflicts<br>- Matches the latest commit | - Requires a robust CI/CD setup<br>- Heavy reliance on senior engineers<br>- Feature flag clutter<br>- Limited traceability  |
| **Git Flow**                     | - Well-suited for staged releases<br>- Ideal for legacy systems<br>- Provides traceability and accountability | - Complex and requires strong DevOps management<br>- Frequent merge conflicts<br>- Longer path to production<br>- Steeper learning curve |
| **Feature Branching**            | - Supports concurrent feature development<br>- Isolates feature work<br>- Reduces risk in main branch<br>- Greater control over feature releases | - Merge conflicts can still occur<br>- Complexity from both Git Flow and Trunk-Based Development<br>- Can delay production readiness |



_The most important thing is to pick a workflow that fits your team and implement it properly. The worst-case scenario is having no workflow, leading to ad-hoc releases with no visibility or accountability._

> Opinion: If you're starting fresh without legacy baggage, I highly recommend using the trunk based workflow. However in practice, using three long-living branches (`main`, `qa`, `develop`) is what lot of teams are comfortable with and makes development smoother specifically if you’re dealing with legacy software or don't have a robust test automation. I am not a big fan of feature branching where the hybrid approach takes on the negatives of both Trunk-Based and Git Flow without enough benefits.

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

> [!IMPORTANT]
> As an early-stage company, **do not start with microservices**, even if you anticipate needing them in the future. Most frameworks are designed to allow you to separate components later, if necessary. Start with a **monolith** on managed services like Heroku, Elastic Beanstalk, or Vercel. Also, use managed databases. While they might be more expensive, it’s worth the peace of mind not having to worry about losing data. 


All major cloud providers offer managed services like **Elastic Beanstalk** or **Heroku**. These services handle a lot of the DevOps overhead for you, so you can focus on building your product. Since they are containerized, you can migrate to **Kubernetes** or your own clusters later if needed.


In the early stages, your goal should be to move fast, deploy features, and find product-market fit. Keep in mind that these decisions will incur **technical debt**, and you’ll likely need to refactor later. But that’s a good problem to have!

> Opinion: I guarantee that if you are deploying your code manually you will end up spending more time than the time it takes to setup CD. In my experience, as you scale, you’ll likely need to **rebuild your product** anyway. The decisions you make at 1,000 users will not hold at 50,000 or 500,000 users. Over-optimizing for scale too early will only slow down your feature development.



## 📊 Monitoring and Error Tracking

_Because relying on your resident superhero to fix everything might make for great stories, but it’s a terrible strategy for your team’s sanity!_

> [!NOTE]
> Avoid the culture where there is one overburdened "maverick" engineer constantly firefighting.Use tools like Sentry and Loggly to make logs and error reports accessible to the entire team without needing production access. Let your team fix issues before they become emergencies.

Error tracking and performance monitoring are often afterthoughts in early-stage companies. Since engineers frequently interact with customers directly, they tend to fix issues as they arise or when users report them.

What typically happens is that one highly skilled engineer—who understands the codebase well—ends up being bombarded with user queries and issues, drastically reducing their productive time. Every startup has that one "maverick" who ends up fixing everything.

While this **maverick (firefighting) culture** is common in startups, it’s extremely counterproductive. The right approach is usually to **fix the issue properly** or let the team handle it without one person constantly jumping in.

This culture arises because there is often **no proper error logging or monitoring**, and only a few people have production access. Even if other team members could fix the issue, the maverick ends up diving in to "save the day." It makes for great stories but results in a terrible developer experience.

#### Fixing the Problem

With the tools available today, solving this issue is straightforward. Pick any central logging tool like **Loggly**, **Papertrail**, or even cloud provider-based logging systems. What’s important is ensuring that the **team** can see production logs without needing direct access to the production servers.

Additionally, use tools like **Sentry**, which can alert the team when an exception occurs. Most frameworks also have built-in error tracking if you prefer not to use third-party tools.

> Opinion: In my teams I have seen the biggest ROI with implementing tools like sentry where crashes are reported (emailed  to the whole team) and a bug is added automatically to your bug tracker. 

Also use tools like **new relic** to keep track of your performance and speed. You don't need to make everything super optimized, but its always a to know what tech improvements can be done when the team has some downtime. 

The goal is to be **proactive** rather than **reactive**.

## 🔒 Security

_Security might feel like an afterthought until one wrong click makes it your only thought._

>[!NOTE]
>Don’t neglect security in early-stage startups. Encrypt sensitive data, use SSL, and manage permissions with group-based controls. Update software regularly, secure cloud storage with encryption, and use password managers with SSO for secure access. Leverage tools like WAFs to block malicious traffic and enforce least privilege principles. Starting early prevents major issues later.

Security often takes a back seat in early-stage startups, but it’s one area you can’t afford to ignore. A single breach could sink your company. Fortunately, basic security practices can significantly reduce your risk with minimal effort.

### Recommended Security Measures

1. **User Authentication**
  Use auth providers like **Auth0**, **Clerk**, or **Firebase** to offload authentication management.

3.  **Group-Based Access Control**  
   Use group-based privileges for access and follow principle of least privilege.

4. **Password Managers & SSO**  
   Use password managers like 1Password or LastPass and implement SSO for secure, centralized authentication.

5. **Secure Cloud Storage (S3, etc.)**  
   Encrypt files, disable public access by default, use signed URLs, and audit permissions regularly.

6.  **Regular Software Updates**  
   Schedule updates every 6 months to patch vulnerabilities and prevent tech debt.

7. **Web Application Firewall (WAF)**  
   Implement WAF to block malicious traffic and exploits.

8. **Encrypt Sensitive Data**  
   Never store passwords in plaintext. Always hash and encrypt data to prevent unauthorized access.

9. **Always Use SSL**  
   Ensure SSL is enabled to protect data in transit.
   


