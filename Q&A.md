# Q1
1. Git is a version control system that tracks changes made to files in a repository. GitHub is a cloud platform that uses Git and stores local repositories online to make it easier to share with others.
2. _git config --list_ shows all configuration settings that are at the current working directory. User.name and user.email matter for commit history and visibility because Git uses this information to record who changed files and what they changed too.
3. _init.defaultBranch_ is a setting that specifies the default name of the first branch when a repository is made. Teams standardized on _main_ for a more clear description of the branch's purpose.
4. 
To set the user.name locally:
* git config user.name "name"  
  
To set the user.email locally:
* git config user.email "email"  

# Q2
1. .venv/ should be excluded from version control because this is where platform specific files are located, which can cause problems on another machine or OS.
2. .gitignore prevents automatic tracking of files listed in the file, but if a file was being tracked earlier, that history is preserved. git rm --cached <file> removes tracking, then it needs to be commited to track the new change.
3. Separating _docs/_, _tests/_, and _ops/_ from application code is useful in a job setting because it organizes files by purpose and makes it easy to navigate and find what one needs.

# Q3
1. See bullet points.
* http://localhost:8080/ - shows the Flask app's home page with a link to /api/health
* http://localhost:8080/api/health - returns JSON of the app's health status
* http://localhost:8080/api/config - returns config.json as a JSON with the app name and version
2. 0.0.0.0 is used instead of 127.0.0.1 because the latter only allows access from the container, while the former allows for access on all available networks.
3. HEAD is the current commit or branch. It tells you where you are in the tracking tree. It is pointing to the current branch, which is pointing towards the recent commit.
4. .gitignore, config.json, docs/APP_RATIONALE.md, docs/ARCHITECTURE.md, ops/README.md, requirements.txt, and test/.gitkeep

# Q4
1. git diff and git diff --staged. 
2. The numbers tell the number of lines removed (red) and the number of lines added (green). The header show which line the changes start.
* ![local screenshot](./Q4_P2_1.png)
* ![local screenshot](./Q4_P2_2.png)
3. Reviewing staged changes will show what will be changed before you commit. This lets you catch errors that may show up and ensure they don't break functionality.

# Q5
1. --no-ff creates a merge preserving the history instead of merging directly into main.
2. git switch -c makes and changes to a new branch, git checkout -b does the same but is older.
3. git log --oneline --graph --decorate shows a commit history with branch names and merge commits, and a graph to visual all the commits, branches, and merges.

# Q6
1. git remote add origin <url> adds the GitHub repo as the remote named origin. Not having this would make git push fail
2. -u sets origin as the upstream tracking branch, so pushes only need git push rather than specifying a location
3. git branch -vv shows each branch, latest commits, and tracking branch. The tracking relationship links branches to remote branches for easier pushing and pulling
4. https://github.com/CNthehuy/flask-devops-lab.git

# Q7
1. See bullet points.
* heading - organizes sections
* code blocks - makes commands easier to read and copy
* lists - presents easier to scan format
2. The README appeared after the git pull. It didn't exist locally because it was added to the cloud repository, so the local repository needed to do a pull to get the updated repository.

# Q8
1. GitHub issues are used to track bugs, feature requests, and tasks. This allows teams to organize and manage work.
2. https://github.com/CNthehuy/flask-devops-lab/issues/1#issue-4772053486
3. GitHub labels categorize issues to make it easier to filter and prioritize work.

# Q9
1. See picture.
![local screenshot](./Q9_P1.png)
2. It closes the issue on GitHub and allows you to close the branch if you choose so.
3. https://github.com/CNthehuy/flask-devops-lab/pull/3#issue-4772114319

# Q10
1. <<<<<<< marks the start of current branch's version, >>>>>>> is the other branch's version, and ======= separates the two versions.
2. git switch -c conflict/a main
git add README.md
git commit -m "docs: version A README change"

git switch -c conflict/b main
git add README.md
git commit -m "docs: version B README change"

git switch main
git merge conflict/a
git merge conflict/b

git add README.md
git commit -m "fix: resolve README merge conflict"
git push origin main

3. git merge --abort cancels conflicted merges and returns the repo to the state before the merge.

# Q11
1. The issue is marked as done/closed, but it doesn't change columns. 
![local screenshot](./Q11_P1.png)
2. https://github.com/users/CNthehuy/projects/2/views/1

# Q12
1. docker version confirms that both the client and daemon are running.
* client - CLI or interface the user interacts with and sends commands to the daemon
* daemon - background application that builds, runs, and manages containers and images
2. /shared.txt wasn't in ubuntu-b because images are immutable unless a volume or bind mount is connected. Docker images are made from multiple read-only layers, which are immutable, so anything saved in an image are on the writable layer which won't be retained. 

# Q13
1. COPY . . copies files from local directory on the host machine to the working directory in the image. It is placed after requirements and pip install because it speeds up build time of the image.
2. Binding to 0.0.0.0 allows for network requests from outside the container to be passed and acted on. 
3. EXPOSE 8080 sets the port that will be used for inbound traffic. It isn't enough to reach the app from the browser because you need to map this port to another port on the host machine, since the EXPOSE refers to the ports on the container.

# Q14
1. Steps 2-5 are cached because these steps have not changed since the last build.
![local screenshot](./Q14_P1.png)
2. .dockerignore matters for speed because it stops docker from including unwanted files like .whl.

# Q15
1. The file persisted because it had a volume specified where it could save written data to. Volumes exist outside the container, so anything saved to it can be used in new instances.
2. A volume and bind mount both store data, but differ in where they store it. Volumes are stored in a location managed by Docker, while bind mounts are stored based on a specified absolute path.

# Q16
1. Compose created flask-devops-lab-app image, flask-devops-lab-default network, flask-devops-lab_app-data volume, and flask-devops-lab-app-1 container. 
![local screenshot](./Q16_P1.png)
2. The -> under the ports section tells you the mapping between host and container ports for the app.
3. docker compose down stops and removes everything made by the up command, but leaves the volumes made. Docker compose down -v stops and removes everything too, but it also removes all volumes in the config file.
![local screenshot](./Q16_P3_1.png)
![local screenshot](./Q16_P3_2.png)
4. docker compose up -d --build forces a rebuild of the image so it has the latest changes, while docker compose up -d can use an older image that isn't up to date.

# Q17 
1. git tag -a v1.0.0 -m "v1.0.0: Flask app containerized with Docker and Compose"
* The -a makes the command annotated.
2. https://github.com/CNthehuy/flask-devops-lab/releases/tag/v1.0.0

# Q18
1. https://github.com/CNthehuy/flask-devops-lab/pull/6
2. Docker images are immutable, meaning the old image contains everything before the PR. If the old image ran, it would work but without the latest features.
3. The benefit is version tracking and the ability to rollback to a stable version if the latest has bugs.

# Q19
1. The flask-app part of the url in docker run --rm --network lab-net curlimages/curl:8.5.0 http://flask-app:8080/api/health.
2. One container is revealed because there is only one container running in the background and attached to the network. 

# Q20
1. A new idea is created as a GitHub issue, then implemented using a Git branch, committed with Git, and pushed to GitHub. This is then reviewed through a Pull Request, and then pulled back into the local repo. A docker image is then built and ran as a container or with compose to check if everything is working as expected.
2. git log --oneline --graph --decorate is more useful than git log because it visualizes the commit history as a graph, showing branches and merges. It also compresses commits into single lines and highlights branch diverges and merges.
3. 
* Git - The most useful concept is branching because it allows for features to be worked on without modifying a stable main branch.
* GitHub - The most useful concept is the projects because it allows for graphical organization of what features are being worked on, what needs to be done, and what is completed.
* Docker - The most useful concept is volumes and bind mounts because most of the time data needs to be worked on and saved for later use.