# Incorrect use of CMD in Dockerfile

This repository demonstrates a common mistake in Dockerfiles: using `CMD` instead of `ENTRYPOINT`.  This can lead to unexpected behavior when running the container.

The original `Dockerfile` uses `CMD` to specify the command to run. This means that if you try to run a different command from the host when running the container, it will override the `CMD` instruction.

The corrected `DockerfileFixed` uses `ENTRYPOINT` to specify the main command, allowing you to append arguments from the host without overriding the main command.

## How to reproduce the bug

1. Build the original Dockerfile: `docker build -t my-app .`
2. Run the container: `docker run my-app`
3. Try running a different command: `docker run my-app python3 /app/another_script.py` (assuming /app/another_script.py exists). The original CMD is overridden.

## How to fix the bug

1. Build the fixed Dockerfile: `docker build -t my-app-fixed -f DockerfileFixed .`
2. Run the container: `docker run my-app-fixed`
3. Try running a different command: `docker run my-app-fixed python3 /app/another_script.py` (assuming /app/another_script.py exists). The ENTRYPOINT is preserved and the command is appended.
