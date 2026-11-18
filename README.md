# cloud-eng-study

Study material for cloud engineering on AWS: hands-on notebooks and quizzes, organised by topic.

## Contents

| Folder | Topic | What is inside |
|---|---|---|
| [`iam/`](iam/) | IAM: Identity and Access Management | [`iam-aws-cli-hands-on.ipynb`](iam/iam-aws-cli-hands-on.ipynb), a hands-on lesson using the AWS CLI (users, groups, roles, access keys, MFA, policies, best practices, exercises)<br>[`iam-quiz.html`](iam/iam-quiz.html), a 30-question quiz (20 on the course content + 10 in the style of the AWS Certified Cloud Practitioner exam) |

## Before you start

- **An AWS account.** IAM itself is free.
- **A user with administrator permissions** and an **access key** for it. Avoid using the root user.
  To create the key: AWS console → **IAM** → **Users** → your user → **Security credentials** → **Create access key** → choose **Command Line Interface (CLI)**. Copy both values; the secret is shown only once.
- The notebook creates a few test resources (a user, a group, a role and a policy) and **deletes them all** in Part 8.

---

## Option A: run the notebook in Google Colab (nothing to install)

The easiest way.

1. Open <https://colab.research.google.com>.
2. **File → Upload notebook** and pick `iam/iam-aws-cli-hands-on.ipynb`.
   Or open it directly: <https://colab.research.google.com/github/joaocalixto/cloud-eng-study/blob/main/iam/iam-aws-cli-hands-on.ipynb>
3. Run the cells in order with **Shift + Enter**. The first cell installs the AWS CLI for you.
4. When asked, paste your access key ID and secret access key into the hidden boxes.

---

## Option B: run the notebook on your computer with VS Code

### 1. Install Python 3.10 or newer

- **macOS:** `brew install python` (or download from <https://www.python.org/downloads/>).
- **Windows:** download from <https://www.python.org/downloads/> and tick **"Add python.exe to PATH"** during the install.
- **Linux:** `sudo apt install python3 python3-venv python3-pip`

Check it: `python3 --version` (on Windows: `python --version`).

### 2. Install the AWS CLI v2

- **macOS:** `brew install awscli`
  or download the installer: <https://awscli.amazonaws.com/AWSCLIV2.pkg>
- **Windows:** download and run <https://awscli.amazonaws.com/AWSCLIV2.msi>
- **Linux:**
  ```bash
  curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o awscliv2.zip
  unzip awscliv2.zip
  sudo ./aws/install
  ```

Check it (open a **new** terminal first): `aws --version`

### 3. Install VS Code and its extensions

1. Install VS Code: <https://code.visualstudio.com/>
2. Open VS Code, go to the **Extensions** panel (`Ctrl+Shift+X` / `Cmd+Shift+X`) and install:
   - **Python** (by Microsoft), id `ms-python.python`
   - **Jupyter** (by Microsoft), id `ms-toolsai.jupyter`, which lets VS Code open and run `.ipynb` files
   - *(optional)* **AWS Toolkit** (by Amazon Web Services), id `amazonwebservices.aws-toolkit-vscode`, to browse your AWS account from VS Code

   Or install them from the terminal:
   ```bash
   code --install-extension ms-python.python
   code --install-extension ms-toolsai.jupyter
   code --install-extension amazonwebservices.aws-toolkit-vscode   # optional
   ```
   If `code` is not found on macOS: in VS Code press `Cmd+Shift+P` → **Shell Command: Install 'code' command in PATH**.

### 4. Get the project and create a virtual environment

```bash
git clone https://github.com/joaocalixto/cloud-eng-study.git
cd cloud-eng-study

python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

### 5. Open and run the notebook

1. In VS Code: **File → Open Folder** → choose `cloud-eng-study`.
2. Open `iam/iam-aws-cli-hands-on.ipynb`.
3. Click **Select Kernel** (top right) → **Python Environments** → pick **.venv**.
4. Run the cells in order with **Shift + Enter**. When asked, paste your keys into the hidden boxes.

> **Windows users:** the notebook's `!` lines are Linux/macOS terminal commands (`grep`, `||`, `2>/dev/null`). Use Google Colab (Option A) or run VS Code inside **WSL** (<https://learn.microsoft.com/windows/wsl/install>).

### Optional: save your keys once with `aws configure`

Instead of typing the keys every time you can store them on your computer:

```bash
aws configure
# AWS Access Key ID:     <your key id>
# AWS Secret Access Key: <your secret>
# Default region name:   eu-west-1
# Default output format: json

aws sts get-caller-identity   # should show your account and user
```

If you do this, you can skip the cell that asks for the keys. **Never commit your keys to Git.**

---

## The quiz

Open `iam/iam-quiz.html` in any browser (double-click the file). Nothing to install.

- One question at a time, with the right answer and a short explanation after each one.
- Choose **All**, **Course** or **Cloud Practitioner style** at the top.
- At the end: your score, results by topic, and a button to retry only the questions you missed.

The Cloud Practitioner-style questions are original practice questions written in the format of the exam. They are not real exam questions.

---

## Clean-up and safety

- Always run **Part 8** of the notebook to delete the test user, group, role and policy.
- Never paste your keys into a cell or commit them. The notebook uses `getpass`, so they are not saved in the file.
- If a key ever leaks: disable it right away in IAM, then create a new one.
