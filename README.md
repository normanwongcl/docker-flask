# Dockerizing flask, postgres, nginx

## Prerequisite

1. Make sure you have the following installed on your machine:

   - git
   - python3
   - pip3
   - docker
   - docker-compose

2. If you are using WSL and ubuntu in your workflow, you can set up everything following this repo: <https://github.com/Klezca/dev-workflow-setup>

## To run this project in docker

```docker
docker-compose up -d --build
```

## Run linter

```docker
# Perform a dry-run of black to check what files will be formatted
docker-compose exec web black project --check

# Run black to format the python code
docker-compose exec web black project

# Run flake8 to check if python styling is enforced
docker-compose exec web flake8 project

```

## Run the tests with coverage (without outputting warnings)

```docker
docker-compose exec web python -m pytest "project/tests" -p no:warnings --cov="project"
```

Code Reference used: <https://testdriven.io/blog/dockerizing-flask-with-postgres-gunicorn-and-nginx/>
