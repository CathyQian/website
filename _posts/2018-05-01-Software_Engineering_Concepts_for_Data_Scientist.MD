---
layout: post
title: Software Engineering Concepts for Data Scientist
date: 2018-05-01
comments_id: 2
---

Data scientists usually need to talk with software engineers or data engineers about model deployment, production or data infrastructure. Therefore, it is quite useful to get to know common concepts in software engineering. Here I collected a list of basic software engineering concepts that may be frequently used by data scientists.

# 1. API

API stands for _Application Programming Interface_. It is a set of subroutine definitions, protocols, and tools to allow communication between various pieces of software or software components.

In plain English, APIs allows you to talk to other software easily. Interface is a place where different software components interact. A Protocol is a set of rules defining how they interact, and a Format defines how they talk to each other. Endpoints provide different functionalities within the same interface.See a good tutorial [here](https://medium.com/@tyteen4a03/how-apis-work-an-analogy-for-dummies-ac6ee1d1671b) for reference.

# 2. Virtual Machine

A virtual machine is a computer file, typically called an image, that behaves like an actual computer. In other words, creating a computer within a computer. It runs in a window, much like any other program, giving the end user the same experience on a virtual machine as they would have on the host operating system itself. The virtual machine is sandboxed from the rest of the system, meaning that the software inside a virtual machine can’t escape or tamper with the computer itself. This produces an ideal environment for testing other operating systems including beta releases, accessing virus-infected data, creating operating system backups, and running software or applications on operating systems they weren’t originally intended for.

Multiple virtual machines can run simultaneously on the same physical computer. For servers, the multiple operating systems run side-by-side with a piece of software called a hypervisor to manage them, while desktop computers typical employ one operating system to run the other operating systems within its program windows. Each virtual machine provides its own virtual hardware, including CPUs, memory, hard drives, network interfaces, and other devices. The virtual hardware is then mapped to the real hardware on the physical machine which saves costs by reducing the need for physical hardware systems along with the associated maintenance costs that go with it, plus reduces power and cooling demand.

See reference [here](https://azure.microsoft.com/en-us/overview/what-is-a-virtual-machine/).

# 3. Virtual Environment

A virtual environment creates an isolated environment for us to install needed packages to run a certain project without disrupting the working environment of other projects. It is a widely used strategy to run multiple data science projects on the same computer.

# 4. Git and GitHub

Git is a centralized version control system that tracks changes to files in a project over time. It typically records what the changes were (what was added? what was removed from the file?), who made the changes, notes and comments about the changes by the changer, and at what time the changes were made. Think of Git and version control like a magic undo button.
 
GitHub is a web hosting service for the source code of software and web development projects (or other text based projects) that use Git. In many cases, most of the code is publicly available, enabling developers to easily investigate, collaborate, download, use, improve, and remix that code. The container for the code of a specific project is called a repository.
For any project, GitHub hosts the main repository, from which contributors can make copies for their own work.
- Repository: Also known as a repo, this is the highest unit of storage. A repository contains one or more branches.
- Branch: A unit of storage that contains the files and folders that make up a project's content set. Branches separate streams of work (typically referred to as versions). Contributions are always made and scoped to a specific branch. All repositories contain a default branch (typically named "master") and one or more branches that are destined to be merged back into the master branch. The master branch serves as the current version and "single source of truth" for the project. It's the parent from which all other branches in the repository are created.

# 5. PowerBI

PowerBI is a business analytics service provided by Microsoft. It aims to provide interactive visualizations and business intelligence capabilities with an interface simple enough for end users to create their own reports and dashboards. 

It was initially released in 2014.

Key components of the Power BI ecosystem comprises: 
- Power BI Desktop 
	The Windows-desktop-based application for PCs and desktops, primarily for designing and publishing reports to the Service.
- Power BI Service 
	The SaaS (software as a service) based online service (formerly known as Power BI for Office 365, now referred to as PowerBI.com or simply Power BI).
- Power BI Mobile Apps 
	The Power BI Mobile apps for Android and iOS devices, as well as for Windows phones and tablets.
- Power BI Gateway 
	Gateways used to sync external data in and out of Power BI. In Enterprise mode, can also be used by Flows and PowerApps in Office 365.
- Power BI Embedded 
	Power BI REST API can be used to build dashboards and reports into the custom applications that serves Power BI users, as well as non-Power BI users.
- Power BI Report Server 
	An On-Premises Power BI Reporting solution for companies that won't or can't store data in the cloud-based Power BI Service.
- Power BI Visuals Marketplace 

# 6. Development and Production

Development is the stage of an application before it’s made public while production is the term used for the same application when it’s made public.

The main workflow for online work is: development -> staging -> production. The reason for the separation is based on the knowledge that you're working on a code-base with a team.

Developers work on bugs and features, these get committed and pushed to a stable development branch. All of these changes get merged into staging which undergoes testing and quality assurance. After this, development is rebased using staging. Then development merges into production when you're ready to deploy.

In development stage, the developers will use dummy data for testing purpose the error reporting function is turned on while in production level the dummy data are removed and real data are added to the database and the error reporting function is disabled as well.

# 7. HTTP/GET/POST
HTTP protocol is the foundation of data communication in world wide web. Different methods of data retrieval from specified URL are defined in this protocol.

HTTP POST: uploading a file or when submitting a completed web server
HTTP GET: retrieve information from the server
