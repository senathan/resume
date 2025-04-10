## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/senathan/resume/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/senathan/resume/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

Great! Here's an updated **Slide 2** with added information about the **AI PoC**, integration steps, and how it fits into the pipeline process:

---

### **Slide 2: AI Integration Vision with AWS Bedrock**

#### **What We Want AI to Do (Next Step)**
- **Current Gap**: Automation handles standard upgrades but struggles with:
  - Failures due to deprecated APIs or breaking changes.
  - Legacy code incompatibilities.
  - Choosing the best upgrade version based on compatibility.

- **AI Vision with AWS Bedrock**:
  - Leverage generative AI to:
    - Analyze failed builds/test logs and suggest fixes.
    - Recommend optimal versions for dependencies based on upgrade success likelihood.
    - Refactor code snippets where APIs have changed.
    - Draft commit messages, PR descriptions, and update documentation.

---

#### **Proof of Concept (PoC) Plan**
- Use a subset of microservices (e.g., ATM API & Audit Logger) for pilot.
- Identify common failure patterns from past upgrade logs.
- Train Bedrock agents to suggest fixes and validate them via automated tests.

---

#### **Integration Steps**
1. **Upgrade Failure Detection**:
   - Jenkins/GitLab detects test failures post dependency upgrade.
2. **Trigger AI Agent (Bedrock)**:
   - Logs and project context passed to AI.
3. **Fix Suggestions**:
   - AI proposes code changes, upgrade path, or test refactoring.
4. **Validation**:
   - Changes tested automatically.
5. **PR Generation**:
   - If success, raise a PR with AI-generated summary.

---

#### **Fit in the Current Process**
- **Before**: Human intervention after pipeline failure.
- **Now with AI**:
  - AI intervenes before human involvement.
  - AI reduces delay between detection and fix.
  - Improves speed, consistency, and learning over time.

---

#### **Tools Involved**
- **CI/CD**: GitLab (future), Jenkins (current).
- **AI**: AWS Bedrock for natural language and code intelligence.
- **Supporting**: Jira, SonarQube, Prisma, Maven/Gradle, Snyk (optional).

---

Would you like me to now turn this into a **well-designed PowerPoint** (.pptx) with animations and visuals (e.g., pipeline flow with AI entry point)?
