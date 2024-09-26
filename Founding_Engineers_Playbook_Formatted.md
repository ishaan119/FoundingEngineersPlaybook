
# Founding Engineer's Playbook

## Introduction

The idea behind this book is personal and something I felt would have helped me when I first became the first engineer of a startup. In my experience, even a lot of startups with good traction and seed funding could benefit from this.

This is not a comprehensive list of to-dos, but just enough to get you started. The whole idea of this book is to understand how to ship things faster and with good quality.

## Code Review

**Boy Scout Rule**: Leave the code better than you found it.

### Key Takeaways
- Agree on style guides and **automate** them.
- Set a clear process for reviewers and PR structure.
- Keep PRs **small** (<200 lines).
- PRs shouldn’t sit open for days—respond **fast**.
- Document important decisions (not in PR comments).
- Stay humble—focus on merging, not ownership.

Code reviews typically become necessary when teams grow, and I've always found that code quality improves when you know someone will review your code. If you're a couple of senior engineers, you might not need formal code reviews, but it’s still good to establish the process early.

If you are the only engineer on the team, you can skip this, but be aware that some form of review adds a lot of value. Reviews can be in the form of pair programming, automated testing, etc.

> **Opinion**: It’s hard to hire senior engineers at early-stage startups, and most of the time, you end up with junior devs. Code reviews or pair programming are a great way to help them improve.

Reviews aren’t just for catching bugs—they're great for sharing best practices and experiences across the team. Plus, it’s **10x cheaper** to catch bugs early instead of in production.

But beware: code reviews can also expose poor culture and unprofessional behavior. If not managed properly, they can slow things down or hurt morale.

Being a good developer doesn’t necessarily make you a good reviewer. Great reviewers:

- Give constructive feedback.
- Know what to prioritize.
- Respond to comments and encourage productive discussions.

Before introducing code reviews, it’s crucial to:

- Agree on a style guide and automate it.
- Set rules for PR size and how long they remain open (no more than 24 hours).

---

## Git Hooks

Git hooks are a hidden gem in every developer’s toolkit. They offer an easy way to automate tasks and improve productivity early on in your project.

### Popular Git Hooks

- **Linting**: Enforce coding standards.
- **File checks**: Ensure no unnecessary files are committed.
- **Commit message formatting**: Maintain consistency.
- **Static analysis**: Catch errors before they enter the codebase.

### Key Takeaways

1. Git hooks are flexible and can be written in any language, as long as they're executable.
2. Implement them early; they don’t affect your existing code and can add tremendous value.
3. Git hooks are for developer productivity and can be bypassed, but tools like GitHub offer paid services to enforce them more strictly.
4. Examples:
   - **pre-commit**: Spell-check commit messages.
   - **pre-receive**: Enforce coding standards before accepting a commit.
   - **post-commit**: Notify the team of new commits via email/SMS.
   - **post-receive**: Push the code to production.

---

## CI/CD

CI/CD is one of the most useful, yet misunderstood, terms in the industry. Many confuse Continuous Integration (CI) with Continuous Delivery/Deployment (CD), but they are distinct.

### Key Differences

- **CI**: Automates code merging, testing, and builds.
- **CD**: Automates deployments to production or other environments.

### Why CI/CD Matters

It’s best to set up CI/CD early when starting a project. It’s much harder to implement it later. GitHub Actions is highly recommended for its community support.

> **Opinion**: Avoid microservices at the early stages. Most frameworks allow separation later on if needed. Focus on building and scaling later.

### Key Takeaways

1. Start with a **monolith** on managed services like Heroku or Elastic Beanstalk.
2. Use managed databases and platforms that remove the need for extensive DevOps.
3. Focus on moving fast and deploying features. Technical debt is inevitable but manageable.

---

## Release Management

Choosing the right release workflow is key to maintaining efficiency as your team grows. Most startups either have an overly complex process or one that’s too simple.

### Workflows

#### Trunk-Based Development

Trunk-based development is ideal for fast-moving teams. It involves short-lived branches that merge directly into the main branch. This workflow requires a robust CI/CD pipeline.

- **Pros**: Simple workflow, always production-ready, fewer merge conflicts.
- **Cons**: Requires senior engineers, feature flag clutter, and limited traceability.

#### Git Flow

Git Flow is best suited for legacy software and structured environments. It uses long-living branches like `develop`, `qa`, and `main`. 

- **Pros**: Great for multiple release versions and compliance needs.
- **Cons**: Complex, with potential merge conflicts and a longer path to production.

#### Feature Branching

Feature Branching strikes a balance between Trunk-Based and Git Flow. It’s ideal for concurrent feature development, with branches merging back into the main.

- **Pros**: Allows parallel development, fewer conflicts.
- **Cons**: Inherits downsides from both Trunk-Based and Git Flow.

---

## Security Best Practices

Security is often overlooked at startups, but a breach can be devastating. Basic security measures can protect your startup from disaster.

### Key Measures

1. **Encrypt Sensitive Data**  
   Never store passwords or sensitive data in plaintext. Always hash and encrypt such data before storing it to prevent unauthorized access.

2. **Always Use SSL**  
   Ensure SSL is enabled on all web traffic to protect data in transit.

3. **Group-Based Access Control**  
   Implement group-based privileges to simplify user management.

4. **Regular Software Updates**  
   Schedule regular updates to avoid technical debt and vulnerabilities.

5. **Secure Cloud Storage (S3, etc.)**  
   Encrypt files in cloud storage, disable public access, and regularly audit permissions.

6. **Use Password Managers & SSO**  
   Use password managers and enable Single Sign-On (SSO) wherever possible to streamline access management and improve security.

7. **Web Application Firewall (WAF)**  
   Use WAFs to block malicious traffic with minimal configuration.

8. **Principle of Least Privilege**  
   Only give users the access they need and no more.

9. **Secure File Uploads**  
   Regularly audit uploaded files to ensure sensitive information isn’t exposed.

---

## Final Thoughts

The most important thing is to pick processes that fit your team and implement them properly. Having no workflow or structure leads to chaos. Set up the right processes early to avoid headaches as your team scales.

---
