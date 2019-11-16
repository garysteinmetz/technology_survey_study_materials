# I Know How To Collaborate with a Team To Edit Source Code

## What Is Source Code?
Source code is all of the base ('raw') material used in a software project - the
files used to create an application. These can include HTML files,
configuration files, test files (including unit tests), build files
(for assembling the project into a single file that can be run),
documentation, and source code files.

### Not Everything that a Project Needs Belongs in the Source Code

Some software project files are purposefully stored elsewhere.

  - Media files (like pictures,
    audio, and movies) might be included, but they're frequently instead
    stored elsewhere in something called a Document Management System.
  - Many computer programming languages, like Java, don't directly
    run the (human-friendly) files programmers create but instead
    'compile' (convert) them into the (computer-friendly) files
    that the computer will actually execute. These compiled files
    aren't considered part of the source code because (A) they
    aren't the 'source' code but a result of the source code
    and (B) these 'compiled' files can always be recreated.
  - Modern software projects make heavy use of third-party libraries.
    Instead of solving the same problems (like a mechanism for changing
    the section of a web page) over and over again with each new project
    ('reinventing the wheel'), software projects ubiquitously import
    third-party libraries (like jQuery) to solve common problems.
    Since these third-party libraries are publicly available,
    there's no need to (redundantly) include them in the source code.
    Using third-party libraries have major advantages including -
      - Instead of spending time solving a problem that's already been
        solved, a developer spends more time on valuable aspects
        of a project.
      - Third-party libraries can have many users and a long track
        record of usage and revision which makes them more reliable
        (e.g. fewer bugs).
      - New hires may know about these libraries and be more
        ready to contribute sooner to a software project which
        uses the libraries.

## Problems with Managing Source Code

Most software projects involve several people and building software
is complicated, so it's important to coordinate the delicate
and detailed process of creating software. Without this coordination,
progress on the software project and even cohesion in the software
development team can quickly become a mess and even break down.

Problems managing the source code include the following.
  - Where should the source code be stored?
  - Who has authority to edit the source code?
  - How can two or more people work on the project at the same time?
  - If newer work is incorrect, how can previously working code be recovered?
  - Software teams frequently maintain (e.g. correct bugs)
    on a published version of the software while adding new features
    to an upcoming release. How can different versions of the software
    project be developed at the same time?

## Where Is Source Code Stored?
Source code is stored in a source-code repository which is either
a file directory containing the source code
(and supporting ('meta') files which contain history
and other information) or a database holding the same information.

## What Is a Popular Source-Code Repository?
Git is an extremely popular source-code repository. It was first
developed in 2005 by a team including the creator of Linux, Linus Torvalds.

## How Is Git Different from Traditional Source-Code Repositories?
Traditional source-code repositories have just one central
location for storing files. Developers copy the files (but not all
of the metadata) to their local systems and submit changes back
to the central repository. As an analogy, the central repository
is like a planet and each developer's computer is like a moon
orbiting around it.

Git is decentralized meaning that there typically is one dedicated
copy of the source code but each developer's computer gets
an entire copy of the repository. As an analogy, each copy of the
repository is like a planet (no moons).

In practice, Git is a lot like traditional source-code repositories,
but it requires that edits first be made ('commit') to one's local
repository before updating ('push') to the main repository.
For traditional source-code repositories, a 'commit' alone is good
enough to update the central repository.

Here is a perspective on Git.
  - Drawbacks
    - Git has a large learning curve. For those who want to
      'just write code' or 'get something done', the complexity
      of Git can seem like an ornate and frustrating distraction.
      For instance, it's a common beginner's error to 'commit'
      changes without issuing a 'push' command.
  - Benefits
    - It tends to be fast, like downloading changes don't hang
      as much as other tools.
    - (Major Benefit) Creating split-off points ('branching') for
      developers to work on is easy and reassembling those
      splits ('merging') is also easy.
    - Git gives users a lot of power of making large yet targeted
      changes to the repository. For instance, if a production password
      accidentally got stored, someone can not only erase it from
      the current version but remove it from the history too.
    - Free online source-code repositories, like GitHub, use Git.
  - Reality
    - Because Git is the most popular source-control repository, an aspiring
      developer should learn how to use it.

Note that for someone who's been in software development
for several years, it's quite common to learn a new tool or framework
which does about the same things as an existing tool or framework
every few years. There's always a quest for a 'better mousetrap',
and two or more valid and competing tools/frameworks which do nearly
the same thing can be popular at the same time. For instance,
since even 1995, developers have been using CVS, SVN,
Visual Source Safe, PVCS, PerForce, ClearCase, and other
source-code repositories.

As potentially unnecessary and redundant as it may seem,
employers and software projects will expect or require a software
developer to know how to use more than one tool/framework even
though just one would be sufficient.

## Git Basics

There are many online tutorials about Git and it takes lots of study
and interest to master it, but here are a few commands that should
allow a developer to interact with it.

With Git, it's important to note that the 'master' branch
generally is the main location of the most up-to-date version
of a software project. A 'branch' is a variation of a project
(e.g. a branch for a new feature, a branch for a maintenance release,
a branch for an upcoming release, a branch which uses
an experimental new framework).

The term 'mark' below means preparing a file to be committed to the local
repository. (Git users use the word 'stage' instead.)

### Get (Clone) a Copy of a Repository
`git clone <repository location>`

### Update the Local Repository
`git fetch --all`

### Update Local Files
`git pull origin master`

Using a 'fetch' followed by a 'pull' ensures that a developer is using
the latest version of the source code.

### Mark a File Ready to Commit
`git add <filename>`

The file can be an existing file that has changed or a new file that's being added.

### Determine Which Local Files Have Been Added, Deleted, Modified, Or Marked for Commit
`git status`

Edits to marked files will be displayed in green.

Edits to unmarked files will be displayed in red.

### Undo Changes on an Unmarked File
`git checkout <filename>`

If the file was deleted it will reappear.

### Mark a File as Deleted
`git rm <filename>`

### Unmark a File
`git reset -- <filename>`

### Commit (Upload) Marked Files to the Local Repository
`git commit -m "<reason for these changes>"`

Without a 'push', other developers won't see the changes!

### Upload Commits to the Remote Repository for Others to Get
`git push origin master`

Now other developers will get the changes (when they issue a 'fetch' then 'pull')!
