# 🛠️ **Build Tools**

A Docker image with essential CI/CD tools optimized for use in GitLab CI pipelines. This image includes powerful utilities for managing builds, scanning vulnerabilities, and automating deployments.

## 🚀 **Tools Included**

- **bash**: Command-line interface for interacting with your system.
- **curl**: Tool for transferring data with URLs.
- **[Docker](https://docs.docker.com/engine/reference/commandline/cli/)**: Containerization platform.
- **[Docker Buildx](https://docs.docker.com/build/architecture/#buildx)**: Advanced build tools for multi-platform builds.
- **[Docker Compose](https://docs.docker.com/get-started/08_using_compose/)**: Define and run multi-container Docker applications.
- **git**: Distributed version control system.
- **openssl**: Toolkit for Secure Sockets Layer (SSL).
- **[regctl](https://github.com/regclient/regclient)**: Advanced image handling (push/pull, manage images).
- **rsync**: Fast and versatile file copying tool.
- **[sshpass](https://www.redhat.com/sysadmin/ssh-automation-sshpass)**: For SSH servers with password authentication.
- **[Trivy](https://aquasecurity.github.io/trivy/)**: Simple and comprehensive container scanner for vulnerabilities.

## 🛠️ **Dependencies**

- **Docker**: Make sure Docker is installed to use the image.

## 🏁 **Getting Started**

To use the image in your CI pipeline, add the following to your `.gitlab-ci.yml`:

```yaml
default:
  image: khulnasoft/build-tools:0.65.0


## Usage examples

### Build images with Docker Compose

Specify `COMPOSE_FILE` if different from the default: `docker-compose.yml`. See [Docker Compose documentation](https://docs.docker.com/compose/compose-file/build/) for more details.

```yaml
build_app:
  variables:
    COMPOSE_FILE: docker-compose.build.yml
  stage: build
  script:
    - docker-compose build app
    - docker-compose push app
```

### 🔍 Run Trivy for Container Scanning

Adjust the image-name and tag after copying the command to your `.gitlab-ci.yml`. See [trivy documentation](https://aquasecurity.github.io/trivy/latest/docs/target/container_image/) for more details.

```yaml
container_scan:
  script:
    - |
      trivy image \
        --severity HIGH,CRITICAL \
        --ignore-unfixed \
        --exit-code 1 \
        registry.gitlab.com/your-repository-path/your-image-name:your-tag
```

## 🤝 Contributing

To release a new version on Docker Hub run:

```bash
export VERSION="0.65.0"

# Init buildx
docker buildx create --use

# Build, tag and push
docker buildx build \
  --platform linux/amd64,linux/arm64/v8 \
  --tag khulnasoft/build-tools:$VERSION \
  --push \
  .
```

## 📜 License

GNU General Public License v3.0

---

Made with ❤️ by [Khulnasoft](https://github.com/khulnasoft)
