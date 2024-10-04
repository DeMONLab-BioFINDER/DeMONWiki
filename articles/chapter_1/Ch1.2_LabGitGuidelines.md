# DeMON lab GitHub Guidelines

---

## General Organization

---

### Motivations

The motivations of maintaining a lab-wise GitHub organization are multifold.

- The codes/scripts of every lab's paper is easy to find/maintain/reproduce;
- The project codes/scripts are version controlled;
- The future labmates could easily follow/reuse codes/scripts;
- ...

### Project-wise (paper-wise) repo

You are recommended to create a project-wise repo for each of your projects. Usually one repo is for one paper, you could discuss with Jake about repo structure if your papers are heavily entangled with each other.

### Recommended repo structure

In general, your repo should cover:

- `func` directory for all your functions/classes;
- `script` directory for all your scripts to call functions/classes in `func` for analysese;
- `data` directory for all your data (pre)processing, split, QC procedures;
- `example` or `tutorial` directory for users to easily run your analyses using fake/public data.

{% hint style="danger" %}
In our lab, most data we used are restricted access. **NEVER PUT YOUR DATA ON CLOUD STORAGE (Github, Dropbox, Google Drive,...)**. It will cause serious problems!
{% endhint %}

### Private mode

You could easily control the visibility level (public/lab-wise/yourself) of your codes by setting access constrain of your project repo.

## Reproducibility

---

In DeMON lab, we strongly support open-science. Every paper's code should be reviewed independently by another co-author (`reproducibility person, RP`) for reducing errors and checking reproducibility.

The procedure of `reproducibility` is conducting by Pull Request.

Before your paper is almost ready (for example, final revision round), you should begin to cleanup your code for being ready to code review.

In general, the `reproducibility` procedure should cover:

- Highly structured code/scripts with clear comments for easy reading;
- Accessible data for `RP` to run your code;
- Detailed comments/checks by `RP`;
- Validation of results:
  - Jupyter Notebook
  - Querto document
  - Output folder/Reference documents

For `RP`, you can give different levels of comments/checks after discussion with Jake, depending on your experience and engagement of project.

- Level1: Successfully running code and pass all results validation checks;
- Level2: Providing coding suggestions;
- Level3: In-depth comments for algorithms/approaches used in this project.

## Documentation

---

Although perfect code is self-explanatory, academy is never perfect. You are highly recommended to have detailed documentations for your project. A user is more likely to try your paper (leading to high impacts) if your project is easy to run/replicate.

You should at least have a top-level `README.md` in your repo with:

- Introduction/Background
- Link of your paper
- Usage
- Contact

For your functions/classes, highly recommended to have `docstring` to describe the `input`, `output`, `expected behavior` of your code.

## Coding guidelines

---

You are highly recommended to think about following points during your coding/refectory:

- Modularity
- Avoid hard coding
- Follow some language-specific guidelines (e.g., `PEP8` for Python)
- Clear and readable code (e.g., meaningful variable names)
- Short functions/scripts (e.g., No one could follow a 2000 lines function)
- Comments for important/complex code blocks
- Progress bar for long running
- No data leakage (e.g., printed out rows in Jupyter Notebook)

## Utilities

---

{% hint style="info" %}
Please stay tuned.
{% endhint %}

# Bugs and questions

---

If you have any questions or find any bugs for this page, you could talk with Jake.
