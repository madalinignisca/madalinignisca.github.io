---
layout: page
title:  "Chapter 1: Getting Started with Python"
date:   2024-02-11 12:12:12
---
- [Introduction to Programming and Python]({{ site.baseurl }}#introduction)
- [Why Choose Python?]({{ site.baseurl }}#why)
- [A Brief History of Python]({{ site.baseurl }}#history)
- [Windows Installation Guide]({{ site.baseurl }}#windows)
- [MacOS Installation Guide]({{ site.baseurl }}#macos)
- [Linux Installation Guide]({{ site.baseurl }}#linux)
- [Choosing a Text Editor or IDE]({{ site.baseurl }}#ide)
- [Running Your First Python Script]({{ site.baseurl }}#script)

## Introduction to Programming and Python {#introduction}

Welcome to the world of programming! If you've picked up this book, chances are you're looking to dive into coding and have chosen Python as your starting point. That's a fantastic choice! This chapter will introduce you to the basics of programming and give you an overview of what makes Python such a popular language among beginners and professionals alike.

*What is Programming?*

At its core, programming is about solving problems. It involves writing instructions that tell a computer how to perform tasks. These tasks can range from something as simple as adding two numbers together, to complex operations like data analysis or building web applications.

When we program, we use languages that computers can understand—these are known as programming languages. Just like human languages have grammar rules and vocabulary, so do programming languages. They consist of syntax (rules about structure) and semantics (meaning).

*Why Learn Programming?*

Learning how to code equips you with the ability to create software applications on your own; it enhances problem-solving skills by teaching logical thinking; it opens up career opportunities in numerous industries; and most importantly, it empowers you with the knowledge to bring your ideas to life through technology.

*An Introduction To Python*

Python is a high-level, interpreted language created by Guido van Rossum and first released in 1991. Its design philosophy emphasizes code readability with its notable use of significant whitespace (more on this later). The simplicity of Python means that anyone can learn it—and many people do!

Here's why Python is an excellent choice for beginners:

- **Readability**: With its clear syntax, reading Python code feels almost like reading English sentences. This reduces the learning curve for new programmers.
  
- **Versatility**: Whether you want work in web development, data science, artificial intelligence or simply automate repetitive tasks—Python has libraries (collections of pre-written code) that make these possible.
  
- **Community Support**: A vast community surrounds Python which means plenty of resources—from tutorials online forums—are available at no cost.
  
- **Cross-platform Compatibility**: You can run python programs on Windows Linux macOS without needing modify them significantly if all

Now let’s get our hands dirty start journey into becoming proficient programmer using one today’s most powerful accessible tools: The wonderful world awaits us!

## Why Choose Python? {#why}

In the vast sea of programming languages, you might wonder why Python has become such a widely recommended language for beginners and experts alike. Here are some compelling reasons that make Python an excellent choice for anyone looking to start their journey in coding:

- **Ease of Learning**: Python's syntax is designed to be intuitive and mirrors the English language to some extent, which makes it more accessible than many other programming languages. This readability means that new programmers can grasp the basics quicker and focus on learning programming concepts rather than getting bogged down by complex syntactical rules.

- **Versatility**: With Python, versatility is your playground. It's used in web development, data science, artificial intelligence, machine learning, automation, game development, cybersecurity—the list goes on. Whatever area you're interested in exploring further down your coding path; chances are there’s a way to do it with Python.

- **Large Community & Support**: A strong community not only helps with problem-solving but also contributes countless modules and libraries—pre-written pieces of code—that extend Python’s functionality exponentially. Whether you’re stuck or need advice on best practices, there’s a global community available 24/7 through forums like Stack Overflow or Reddit.

- **Career Opportunities**: Proficiency in Python opens doors to numerous career paths due to its widespread use across industries. Companies value employees who can harness the power of this flexible tool for various applications from automating mundane tasks to extracting insights from big data sets.

- **Cross-platform Nature**: Write once; run anywhere—Python is cross-platform which means that generally speaking (with consideration for environment-specific dependencies), if you write a program on one operating system like Windows, it should work just as well on macOS or Linux without significant changes.

- **Rich Ecosystems For Data Science And Machine Learning**: If data analysis interests you then look no further! Libraries such as NumPy Pandas TensorFlow Scikit-Learn have made possible analyze large datasets build predictive models using few lines code thanks robust ecosystem built around these disciplines within community!

By choosing learn python embarking upon exciting adventure where creativity meets logic possibilities endless let's begin our exploration together starting very fundamentals!

## A Brief History of Python {#history}

To appreciate the language you're about to learn, it's helpful to know a bit about its origins and evolution. Python was conceived in the late 1980s by Guido van Rossum at Centrum Wiskunde & Informatica (CWI) in the Netherlands as a successor to the ABC programming language, which was inspired by SETL.

- **The Birth of Python**: The implementation of Python began in December 1989. Van Rossum aimed to create an easy-to-read, high-level programming language that allowed users express concepts in fewer lines of code than languages like C++ or Java. The name 'Python' was influenced by Guido's favorite comedy group, Monty Python’s Flying Circus.

- **Python 1.0**: In January 1994, Python reached version 1.0 status with core features such as exception handling and functions like lambda, map, filter and reduce.

- **Python 2.x**: Released on October 16th, 2000 with many major new features including a cycle-detecting garbage collector for memory management and support for Unicode.

- **Transition from Python 2 to Python 3**: One significant moment in the history of this language came when it made a challenging transition from version two to three. With the release of Python 3.0 in December of that year—also known as "Python3000" or "Py3k"—the community decided not just improve upon but rather redesign certain parts language make more powerful robust However because these changes were not backward compatible they required programmers adapt their old codebase work new system This process took years is still ongoing some areas today!

- **Steady Growth**: Over time has grown exponentially popularity due much part its simplicity flexibility It consistently ranks among top programming languages world according various indexes surveys

Today continues be developed maintained by diverse team volunteers around globe under auspices non-profit organization Foundation (PSF) Whether you're interested web development scientific computing artificial intelligence anything else between there's good chance will tool need succeed Welcome aboard journey through rich engaging landscape – let’s get started!

## Windows Installation Guide {#windows}

Installing Python on a Windows machine is straightforward. Follow these steps to set up your environment and start coding.

*Step 1: Download Python*

1. Go to the official Python website at [python.org](https://www.python.org/).
2. Hover over the "Downloads" tab and click on "Windows".
3. Click on the latest version of Python to download it (as of this writing, that would be Python 3.x). You can usually find this under the “Stable Releases” section.
4. Choose either the 32-bit or 64-bit installer based on your system's architecture. If you're unsure which one you need, most modern computers are 64-bit.

*Step 2: Run Installer*

1. Once downloaded, locate the file (typically in your Downloads folder) and double-click it to run the installer.
2. Before proceeding with installation:
   - Check the box that says **“Install launcher for all users (recommended)”**.
   - Also check **“Add Python x.x to PATH”** at the bottom of the window before continuing; this step is crucial as it allows you to run Python from Command Prompt without specifying its full path.
3. Click “Install Now”.

*Step 3: Verify Installation*

After installation completes:

1. Open Command Prompt by typing `cmd` into your search bar and hitting Enter.
2. In Command Prompt, type `python --version` and press Enter.
   
   This command should return something like:
   
   ```
   Python x.x.x
   ```
   
If you see a version number, congratulations! You've successfully installed Python.

*Optional Step: Install pip (if not included)*

pip is a package manager for installing and managing software packages written in Python.

To check if pip was installed:

1) Type `pip --version` in Command Prompt and hit Enter.

If pip was installed correctly, you'll see a version number returned here too.

Should there be any issues during installation or running these commands after setup, refer back to python.org for troubleshooting advice or consult Appendix A 'Troubleshooting Common Issues' later in this book!

Now that we have our development environment ready let’s move forward learning basics programming with exciting language!

## MacOS Installation Guide {#macos}

Installing Python on macOS can be done in a couple of ways: using the official installer from the Python website or via Homebrew, which is a package manager for macOS. It's important to note that macOS comes with Python pre-installed, but this system version should generally not be used for development as installing packages globally could interfere with the operating system.

**Using The Official Installer**

*Step 1: Download Python*

1. Navigate to [python.org](https://www.python.org/).
2. Hover over "Downloads" and click on "macOS".
3. Click on the latest release of Python to download it.
4. Once downloaded, open the `.pkg` file you just downloaded.

*Step 2: Run Installer*

1. Follow through the installation steps provided by the setup wizard.
2. Make sure to select “Install for all users” if prompted and agree to terms of service when asked.

*Step 3: Verify Installation*

To verify that Python installed correctly:

1) Open Terminal (you can find it using Spotlight with `Cmd + Space` and typing 'Terminal').
   
2) Type `python3 --version` and press Enter (note we use python3 here since macOS refers to its own version of python as `python`, which is typically a 2.x version).

You should see something like:
```
Python x.x.x
```

If you do, then you've successfully installed Python!

**Using Homebrew**

If you already have Homebrew installed:

*Step 1: Install Homebrew (if necessary)*

If you don't have Homebrew yet:

- Open Terminal.
- Paste `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"` into your terminal window and hit Enter.
- Follow any additional instructions presented in Terminal.

*Step 2: Install Python Using Brew*

With Homebrew ready:

- In Terminal type `brew install python`.
  
This command will fetch the latest version of Python from Brew's repositories along with pip.

*Step 3: Verify Installation*

Verify your installation by typing `python3 --version`. You should see a similar output indicating that both are now available on your machine.

Remember not to use sudo when installing packages with pip; instead use virtual environments (`venv`) or user-specific installations (`pip install --user <package>`). This practice prevents potential conflicts between system dependencies and those required by different projects or tools being developed.

Now that we've set up our environment properly let’s proceed learn more about how write code!

## Linux Installation Guide {#linux}

On Linux, Python is often pre-installed with the operating system. However, depending on your distribution and its release date, you might not have the latest version. It's also worth noting that while rolling release distributions will generally provide the newest versions of software, long-term support (LTS) releases may prioritize stability over having the absolute latest.

Here’s how to ensure you have a recent version of Python installed on your Linux machine:

**Checking Your Current Version**

Before installing or updating Python, check what version you currently have:

1. Open Terminal.
2. Type `python3 --version` and press Enter.

If it returns a version number that's 3.x and fairly recent (e.g., within the last year or so), then you likely don't need an upgrade for beginner purposes.

**Installing Python on LTS Distributions**

If your current LTS distribution doesn’t come with a recent enough version of Python or if it isn't installed at all:

*Step 1: Update Package List*

- Open Terminal.
- Run `sudo apt update` to update package lists (for Debian-based systems like Ubuntu).

*Step 2: Install Software Properties Common*

- Run `sudo apt install software-properties-common`.

*Step 3: Add Deadsnakes PPA*

Deadsnakes is a PPA containing more recent versions of Python.

- Run `sudo add-apt-repository ppa:deadsnakes/ppa`.
  
*Step 4: Install Latest Version Of Python*

- After adding new PPAs always run `sudo apt update` again.
- Then install python by running `sudo apt install python3.x`, replacing x with the sub-version number available in repository.

For non-debian based distributions such as Fedora or openSUSE replace 'apt' commands with their respective package management commands (`dnf`, `zypper`, etc.).

**Using Virtual Environments**

Regardless of how you've installed Python, using virtual environments (`venv`) is recommended when developing projects. This isolates project-specific dependencies from global ones which can help prevent conflicts between packages required by different projects.

To create use virtual environment follow these steps after navigating terminal window directory where want work:

1) Create venv folder within project directory by typing:
```
python3 -m venv my_project_venv
```

2) Activate environment:
   - On bash/zsh shells type:
     ```
     source my_project_venv/bin/activate
     ```
   - For csh/fish shells type:
     ```
     source my_project_venv/bin/activate.csh
     ```

Once activated prompt will change indicate are now working inside The changes made here won’t affect rest system

Remember due security reasons '`pip install --user`' has been disabled some distros If encounter issues try alternatives like mentioned above 

Now ready begin exploring capabilities further!

## Choosing a Text Editor or IDE {#ide}

When you're starting out with Python, one of the first things you'll need is a place to write your code. A text editor or an Integrated Development Environment (IDE) provides this space along with many other features that can help streamline your coding process.

*Text Editors vs. IDEs*

A **text editor** is a lightweight program that allows you to write and edit text. When used for coding, they typically offer syntax highlighting and some level of auto-completion but are generally less feature-rich than an IDE.

An **IDE**, on the other hand, includes not only a text editor but also integrates several developer tools such as debuggers, file managers, version control systems, and automated build processes all within one interface.

For beginners in Python:

- **PyCharm Community Edition**: This free version of PyCharm by JetBrains offers powerful features like intelligent code completion, on-the-fly error checking and quick-fixes, easy project navigation, and more. It's tailored specifically for Python development which makes it ideal for beginners who might later transition into using its paid edition for professional work.

  To get started:
  
  1) Download PyCharm Community Edition from [JetBrains](https://www.jetbrains.com/pycharm/download/#section=windows).
  
  2) Follow the installation instructions provided.
  
  3) Once installed open PyCharm create new project ensure interpreter settings correct point towards local python installation
  
- **Visual Studio Code (VS Code)**: VS Code is another popular choice among developers due to its versatility across multiple languages including Python. It’s free open-source maintained Microsoft

   Setting up VS Code with Python support involves installing the official extension developed by Microsoft:

   *Step 1: Install Visual Studio Code*
   
   - Download install VSCode from [code.visualstudio.com](https://code.visualstudio.com/).

   *Step 2: Install The Python Extension For Visual Studio Code*
   
   - Open VSCode.
   
   - Go to Extensions view by clicking on the square icon in sidebar searching "Extensions" at top View menu
   
   - Search “Python” find official extension published Microsoft click install button beside it
   
The extension adds rich support for language including features such as IntelliSense linting debugging unit testing Jupyter Notebooks 

After setting up chosen editor familiarize yourself layout try writing running simple scripts As become comfortable environment will start appreciate how much easier these tools make process learning programming!

## Running Your First Python Script {#script}

Now that you have Python installed and your text editor or IDE set up, it's time to write and run your first script. Instead of the traditional "Hello World" example, let’s create something slightly more interactive—a program that asks for your name and then greets you.

*Step 1: Create Your Script*

Open your chosen text editor or IDE:

- If using **PyCharm**, select “Create New Project”, give it a name like `MyFirstScript`, choose an interpreter (which should be the Python version you've installed), and click “Create”. Inside the project, right-click on the folder with the same name as your project in PyCharm's file explorer pane, select “New” → “Python File”, name it `greet.py`.

- For **VS Code**, open it up and simply go to "File" → "New File". Save this new file with a `.py` extension by going to "File" → "Save As..." and naming it `greet.py`.

In either case, enter the following code into your new file:

```python
# greet.py

def greet(name):
    return f"Nice to meet you, {name}!"

if __name__ == "__main__":
    user_name = input("What is your name? ")
    greeting = greet(user_name)
    print(greeting)
```

This simple script defines a function called `greet()` which takes an argument called `name`. It returns a greeting string including whatever name was passed in. The last three lines make sure that when we run our script directly (and not import from another one), we prompt for input with `input()`, call our function with what we get back from input(), then print out result.

*Step 2: Run Your Script*

To execute this script:

- In **PyCharm**, right-click anywhere in the text editor window where you’ve written code select option says ‘Run 'greet'’.

- With **VS Code**, ensure terminal panel visible at bottom screen if not can toggle view Terminal menu bar Then navigate directory containing saved type command:
  
  ```bash
  python3 greet.py
  ```

Press Enter after typing command see output displayed within integrated terminal itself!

You should now see prompt asking for Name After entering yours press Enter greeted personalized message!

Congratulations! You've just written executed very own custom Python program From here possibilities endless start exploring all sorts capabilities language has offer Happy coding!


[Preface]({{ site.baseurl }}{% link books/python/for-newbies/preface.md %}) \|
[TOC]({{ site.baseurl }}{% link books/python/for-newbies/index.md %}) \|
[Chapter 2]({{ site.baseurl }}{% link books/python/for-newbies/chapter-02.md %})