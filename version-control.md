# Version Control

Version control is a system that records changes to a file or set of files over time so that you can:

- Undo mistakes - keeps track of all your changes in time.
- Work concurrently with a team of people without affecting each other's code.
- Work concurrently on different versions of a project - develop and test new features without affecting a working project.

## Repositories & Working Copies

- A version control uses a repository, which is a database of all project changes, and a working copy (checkout), which is a personal copy of all the files in the project.
- Changes are made to the copy, without affecting the teammates.
- When done, changes are committed to the repository.

## Workflow

- Update your copy from the server.
- Make your changes, & make sure they work properly.
- Commit your changes to the server.

## Version Control Types

![[version-control-types.png]]

### Centralized Version Control Systems

System consisting of a single server that contains all the versioned files, and a number of clients that check out files from that central place. For many years, this has been the standard for version control.

**Advantages**

- One person can control it.
  - It is easier to administer a CVCS than to deal with local databases on every client.
- A master copy of the code is kept centrally.
  - To a certain degree, everyone knows what others are doing on the project.

**Disadvantages**

- What will happen if the server goes down?
  - No one can collaborate nor save versioned changes.
- What if the hard disk with the central database becomes corrupted?
  - If proper backups haven’t been kept, you lose everything.

### Distributed Version Control Systems

In a DVCS, clients fully mirror the the repository. If any server dies, any of the client repositories can be copied back to the server to restore it.

## Version Control Concepts

### Repository

- Location were all versioned products are stored.
- Can be a structured directory on a server with each versioned file stored separately.
- Can be a database containing entries for the various files in a project.
- Can be a complex distributed system that redundantly stores the versioned project in many places.

### Working Directory

- Developers do not work on the files in the repository, but on a copy called as working directory accessible locally on their development machine.
- Once done with the work, the developer commits the changes back into the repository where other developers now have access to them.

### Revisions

- The system does not only store the most recent snapshot of a project many snapshots are stored over time.
- A committed change (snapshot) to a repository is referred to as a revision.

### Logs

- Enable you to keep track of what has been changed, when and why.

### Tagging

- Marking revisions so they can be referred back to at a later time.
- Usually you mark revisions at milestones to make it easier to go back and search out the cause of a newly discovered bug.

### Branching

- Allows creating additional paths of development in a repository (for example, implementing and testing a feature of a project).
- Each branch is worked on independently including commits only affecting the branch they are made on.
- Branches can be merged if needed.

### Merging

- Version control checks for collisions on commits and attempts to automatically merge the file. If not possible, provides the developer with ability to merge changes manually.
