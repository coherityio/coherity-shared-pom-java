# Coherity Shared Parent POM for Java Projects

A comprehensive parent POM that provides standardized dependency management, plugin configurations, and build settings for all Coherity Java projects.

## 🚀 Features

- **Java 21** - Latest LTS version with modern language features
- **JUnit 5** - Modern testing framework with Jupiter engine
- **Updated Dependencies** - Latest stable versions of Apache Commons, Mockito, SLF4J
- **Maven Wrapper** - No need to install Maven locally
- **Code Coverage** - JaCoCo integration for test coverage reports
- **Security Scanning** - OWASP dependency vulnerability checks
- **Automated Publishing** - GitHub Actions workflow for artifact delivery

## 📦 Usage

### Using as Parent POM

Add this as your parent POM in your project's `pom.xml`:

```xml
<parent>
    <groupId>io.coherity.shared.parent</groupId>
    <artifactId>parent-pom-java</artifactId>
    <version>1.0.0-SNAPSHOT</version>
</parent>
```

### Building Locally

This project uses Maven Wrapper - no need to install Maven:

```bash
# Windows
.\mvnw clean install

# Unix/Linux/macOS  
./mvnw clean install
```

## 🔧 Dependencies Included

| Dependency | Version | Purpose |
|------------|---------|---------|
| JUnit Jupiter | 5.11.0 | Testing framework |
| Mockito | 5.14.0 | Mocking framework |
| Apache Commons Lang3 | 3.17.0 | Utility classes |
| Apache Commons IO | 2.16.1 | I/O utilities |
| Apache Commons Collections4 | 4.4 | Collection utilities |
| SLF4J | 2.0.16 | Logging facade |
| Logback | 1.5.7 | Logging implementation |

## 🏗️ Build Plugins

| Plugin | Version | Purpose |
|--------|---------|---------|
| Maven Compiler | 3.13.0 | Java compilation |
| Maven Surefire | 3.5.0 | Unit test execution |
| JaCoCo | 0.8.12 | Code coverage |
| Maven Wrapper | 3.3.2 | Self-contained builds |

## 🚀 CI/CD Pipeline

### GitHub Actions Workflow

The project includes a comprehensive GitHub Actions workflow (`.github/workflows/publish-pom.yml`) that:

1. **Validates** the POM structure and dependencies
2. **Publishes snapshots** on pushes to `main`/`develop` branches  
3. **Publishes releases** on version tags (`v*`)
4. **Publishes to GitHub Packages** as alternative distribution
5. **Signs artifacts** for release builds
6. **Creates GitHub releases** automatically

### Required Secrets

Configure these secrets in your GitHub repository:

```bash
MAVEN_USERNAME=your-nexus-username
MAVEN_PASSWORD=your-nexus-password  
GPG_PRIVATE_KEY=your-gpg-private-key
GPG_PASSPHRASE=your-gpg-passphrase
```

### Repository URLs

Update the repository URLs in `pom.xml` properties:

```xml
<properties>
    <coherity.releases.repo.url>https://your-nexus-server.com/repository/maven-releases/</coherity.releases.repo.url>
    <coherity.snapshots.repo.url>https://your-nexus-server.com/repository/maven-snapshots/</coherity.snapshots.repo.url>
</properties>
```

## 📋 Publishing Process

### Snapshot Releases (Automatic)

Snapshots are automatically published when code is pushed to `main` or `develop`:

```bash
git push origin main
# → Triggers automatic snapshot publishing
```

### Production Releases

1. **Create and push a version tag:**
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```

2. **GitHub Actions will automatically:**
   - Update POM version to match tag
   - Build and sign artifacts
   - Deploy to Maven repository
   - Create GitHub release
   - Publish to GitHub Packages

### Manual Publishing

For manual publishing (development/testing):

```bash
# Deploy snapshot
./mvnw clean deploy

# Deploy to GitHub Packages
./mvnw clean deploy -Dgithub.packages=true
```

## 🔐 Security & Signing

### GPG Signing

Release artifacts are automatically signed using GPG. Set up GPG keys:

1. Generate GPG key pair
2. Export private key: `gpg --export-secret-keys --armor KEY_ID`
3. Add to GitHub secrets as `GPG_PRIVATE_KEY`
4. Add passphrase as `GPG_PASSPHRASE`

### Vulnerability Scanning

The workflow includes OWASP dependency vulnerability checks:

```bash
# Run security scan locally
./mvnw org.owasp:dependency-check-maven:check
```

## 🛠️ Local Development

### Maven Settings

Use the provided `settings-template.xml` as a starting point:

```bash
# Copy template to Maven settings directory
cp settings-template.xml ~/.m2/settings.xml

# Update with your credentials
vim ~/.m2/settings.xml
```

### Environment Variables

For local development, set these environment variables:

```bash
export MAVEN_USERNAME=your-username
export MAVEN_PASSWORD=your-password
```

## 📊 Usage in Child Projects

Child projects inheriting from this POM get:

- ✅ Java 21 compilation
- ✅ JUnit 5 testing setup  
- ✅ Modern dependency versions
- ✅ Code coverage reporting
- ✅ Standardized plugin configurations

Example child project POM:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    
    <modelVersion>4.0.0</modelVersion>
    
    <parent>
        <groupId>io.coherity.shared.parent.reactor</groupId>
        <artifactId>master-pom</artifactId>
        <version>1.0.0</version>
    </parent>
    
    <groupId>com.example</groupId>
    <artifactId>my-service</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    
    <!-- Your project-specific dependencies -->
    <dependencies>
        <!-- JUnit and Mockito are already included -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
    
</project>
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📜 License

This project is licensed under the terms specified in the LICENSE file.

## 🏢 Coherity.io

Developed and maintained by the Coherity.io team.

For questions or support, please contact the development team.
