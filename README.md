![Codebuild CI](https://codebuild.ap-southeast-2.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiQThZQy9jNkdDdGlwaUJaK3BPR3p1WHBKS0VqRGJHby9WTFExS3ZSdzVwZkNWNEVxaWlOMWE0aWR5dERPWnhnUTNEMC9rU0pxZDBXU0dzT3NhVUR3ampvPSIsIml2UGFyYW1ldGVyU3BlYyI6Ii9qOHZjSGwxaUNGLytDSUMiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=master)

# Dockerizing flask, postgres, nginx

Teaching myself how to work with flask project.

## Prerequisite

1. Make sure you have the following installed on your machine:

   - git
   - python3
   - pip3
   - docker
   - docker-compose

2. If you are using WSL and ubuntu in your workflow, you can set up everything following this repo: <https://github.com/Klezca/dev-workflow-setup>

## To run this project in docker

```bash
docker-compose up -d --build
```

## To run this project in venv

```bash
# Build venv
python3.8 -m venv env

# Run venv
source env/bin/activate
```

## Run linter

```bash
# For docker workflow

# Perform a dry-run of black to check what files will be formatted
docker-compose exec web black project --check

# Run black to format the python code
docker-compose exec web black project

# Run isort to sort import library
docker-compose exec -T web /bin/sh -c "isort project/*/*.py --check-only"

# Run flake8 to check if python styling is enforced
docker-compose exec web flake8 --ignore=E501,F401 project
```

```bash
# For venv workflow

# Run black to format the python code
black services/web/project

# Run isort to sort import library
isort services/*/*/*.py

# Run flake8 to check if python styling is enforced
flake8 --ignore=E501,F401 services/web/project
```

## Run the tests with coverage (without outputting warnings)

```docker
docker-compose exec web python -m pytest "project/tests" -p no:warnings --cov="project"
```

Code Reference used: <https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/>
