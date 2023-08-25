# secret-clean-repo

This is copy of the [secret-leaking-repo](https://github.com/highb/secret-leaking-repo).
Where all secrets have been removed using `git-filter-repo` by following the docs [provided by GitHub](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/removing-sensitive-data-from-a-repository).

Specifically, the following commands were used to remove all secrets from the repo:

```bash
[11:13:32]❮ gh repo clone highb/secret-clean-repo
Cloning into 'secret-clean-repo'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 15 (delta 3), reused 15 (delta 3), pack-reused 0
Receiving objects: 100% (15/15), done.
Resolving deltas: 100% (3/3), done.

[11:13:35]❯ cd secret-clean-repo

[11:13:38]❯ git filter-repo --invert-paths --path secret.env --path secret.json --path secrets.bak.new/test.env
Found existing alias for "git". You should use: "g"
Parsed 4 commits
New history written in 0.18 seconds; now repacking/cleaning...
Repacking your repo and cleaning out old unneeded objects
HEAD is now at 25682d7 Create README.md
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 12 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (12/12), done.
Total 12 (delta 2), reused 6 (delta 2), pack-reused 0
Completely finished after 0.40 seconds.

[11:13:42]❯ echo "secret.env" >> .gitignore

[11:14:11]❯ echo "secret.json" >> .gitignore

[11:14:14]❮ echo "secrets.bak.new/test.env" >> .gitignore

[11:14:39]❯ git add .gitignore
Found existing alias for "git add". You should use: "ga"

[11:14:40]❯ gc
[main 0b41111] Add secret paths to .gitignore
 1 file changed, 3 insertions(+)
 create mode 100644 .gitignore

[11:14:50]❯ glo
0b41111 (HEAD -> main) Add secret paths to .gitignore
25682d7 Create README.md
d7feefb (tag: v2020.0.0) Migrate to the cloud 😎
b6bb1c4 URGENT PRODUCTION FIX
c41ed43 (tag: v1.0.0) Initial commit of script

[11:14:56]❯ git show b6bb1c4
Found existing alias for "git show". You should use: "gsh"
commit b6bb1c46f3be50d5db89d3fa52c81f76c28fa2e1
Author: Brandon High <highb@users.noreply.github.com>
Date:   Fri Aug 25 10:56:01 2023 -0700

    URGENT PRODUCTION FIX


Δ main.py
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

──────────────────────────────────────────────────────────────────────────────────────┐
• 30: encrypted_secret_data = base64.b64encode(encrypted_secret_data).decode("utf-8") │
──────────────────────────────────────────────────────────────────────────────────────┘
# POST the encrypted data to the server

# This is the URL of the server
url = "https://example.com/api"
url = "https://example.com/api/secret"

# This is the JSON payload that will be sent to the server
payload = {

[11:15:02]❯ git show d7feefb
Found existing alias for "git show". You should use: "gsh"
commit d7feefb840de9f6d942b0be861ec654f0d9ee67f (tag: v2020.0.0)
Author: Brandon High <highb@users.noreply.github.com>
Date:   Fri Aug 25 10:58:18 2023 -0700

    Migrate to the cloud 😎


Δ main.py
─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────

──────────────────────────────────────────────────────────────────────────────────────┐
• 30: encrypted_secret_data = base64.b64encode(encrypted_secret_data).decode("utf-8") │
──────────────────────────────────────────────────────────────────────────────────────┘
# POST the encrypted data to the server

# This is the URL of the server
url = "https://example.com/api/secret"
url = "https://cloud.example.com/api/secret"

# This is the JSON payload that will be sent to the server
payload = {

[11:15:59]❯ gr add origin https://github.com/highb/secret-clean-repo

[11:16:01]❯ git push origin --force --all
Found existing alias for "git push". You should use: "gp"
Enumerating objects: 14, done.
Counting objects: 100% (14/14), done.
Delta compression using up to 12 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (12/12), 1.42 KiB | 1.42 MiB/s, done.
Total 12 (delta 2), reused 8 (delta 1), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 1 local object.
To https://github.com/highb/secret-clean-repo
 + 1b08044...0b41111 main -> main (forced update)
```
