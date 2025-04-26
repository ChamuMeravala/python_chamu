import subprocess
import os

def clone_git_repo(github_id, repo_name, branch_name, filename):
    repo_url = f"https://github.com/{github_id}/{repo_name}.git"

    print(f"Cloning repository from {repo_url}...")
    subprocess.run(["git", "clone", repo_url], check=True)

    print(f"Changing directory to '{repo_name}'...")
    os.chdir(repo_name)

    print(f"Setting Git identity...")
    subprocess.run(["git", "config", "user.name", "ChamuMeravala"], check=True)
    subprocess.run(["git", "config", "user.email", "chamundeswari.meravala@gmail.com"], check=True)

    print(f"Creating and switching to branch '{branch_name}'...")
    subprocess.run(["git", "checkout", "-b", branch_name], check=True)

    print(f"Creating file '{filename}'...")
    with open(filename, "w") as f:
        f.write("Hi you can do it, you will do it.")

    print(f"Adding '{filename}' to Git staging...")
    subprocess.run(["git", "add", filename], check=True)

    print("Committing changes...")
    subprocess.run(["git", "commit", "-m", "Add file via Python script"], check=True)

    print(f"Pushing branch '{branch_name}' to remote...")
    subprocess.run(["git", "push", "-u", "origin", branch_name], check=True)

    print("Done! Your changes have been pushed to GitHub.")

if __name__ == "__main__":
    clone_git_repo("ChamuMeravala", "python_chamu", "develop", "chamu.txt")
