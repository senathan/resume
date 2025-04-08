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


Sure! Here's your updated **2-page presentation content** in **layman-friendly terms**, **removing the "My Role & Contribution" section**, and keeping it crisp, professional, and suitable for an AI Architect audience.

---

### **📄 Page 1: Project Summary and Details**

---

#### **📌 Project Title:**  
**Automated Dependency Upgrades & Vulnerability Fixes for Java Applications**

---

#### **🧩 Purpose:**  
To create a system that automatically checks for outdated software components (dependencies) in Java projects, upgrades them to newer versions, and makes sure everything still works — reducing the risk of security problems and saving a lot of manual effort.

---

#### **🛑 Problem Statement:**  
Most large applications use many open-source libraries. These libraries get updated regularly to fix bugs and security issues. But:
- Manually upgrading them is time-consuming.
- It often breaks things if not tested properly.
- Developers delay upgrades because it takes too long.
- Security teams push for fixes, but without automation, it's hard to keep up.

---

#### **✅ Solution:**  
We built an automated pipeline using Jenkins that:
- Checks your project and figures out which parts need upgrading.
- Starts with the main library (like Spring Boot) and tries newer versions one by one until everything passes the tests.
- Skips any upgrades you specifically tell it to ignore.
- Runs security scans.
- Raises a pull request if everything looks good.

It works for both **Maven** and **Gradle** projects and helps keep your application secure and up-to-date without much manual work.

---

#### **📊 Results/Benefits:**  
- Saves **6–8 hours per upgrade cycle**.
- Helps avoid **human errors**.
- Ensures **faster and safer updates** to key libraries.
- Used regularly (every quarter) by **ATM API project** to fix Prisma vulnerabilities.
- Can be applied to **any app** using Maven or Gradle.

---

### **📊 Page 2: Data and Tools**

---

#### **📈 Data (Metrics and Insights):**

| Area | Info |
|------|------|
| Projects Using It | 10+ |
| Time Saved | ~6–8 hours per upgrade |
| Automation Coverage | Parent, child, common dependencies |
| Upgrade Logic | Smart fallback (tries higher to lower) |
| Usage Frequency | Quarterly (e.g. ATM API for Prisma fixes) |
| Build Tools Supported | Maven & Gradle |
| Deployment Target | aPaaS |

---

#### **🛠 Tools Used / Planned:**

| Purpose | Tool/Tech |
|---------|-----------|
| Pipeline | Jenkins |
| Version Detection | Maven Plugin / Gradle Script |
| Code Hosting | Bitbucket |
| Security Scans | Prisma |
| Testing | JUnit, Integration Tests |
| Ticketing | Jira |
| Logging & Tracking | Stash, PR Comments |
| Roadmap | Add support for Python Pip, Docker tools |
| Long-Term Plan | Use AI to auto-suggest fixes & test compatibility |

---

Would you like this converted into a polished **.pptx file with design and animation**? I can prepare and share it directly.
