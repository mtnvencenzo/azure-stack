# 🔒 Security Policy

## 🛡️ Supported Versions

We release patches for security vulnerabilities. Which versions are eligible for receiving such patches depends on the CVSS v3.0 Rating:

| Version | Supported          |
| ------- | ------------------ |
| 1.x.x   | :white_check_mark: |
| < 1.0   | :x:                |

## 🚨 Reporting a Vulnerability

The Azure Stack team takes security bugs seriously. We appreciate your efforts to responsibly disclose your findings, and will make every effort to acknowledge your contributions.

### Where to Report

**Please do not report security vulnerabilities through public GitHub issues.**

Instead, please report them to the maintainer [@mtnvencenzo](https://github.com/mtnvencenzo)

### What to Include

To help us better understand the nature and scope of the possible issue, please include as much of the following information as possible:

- 🎯 **Type of issue** (e.g., container escape, exposed credentials, insecure defaults, etc.)
- 📁 **Full paths of source file(s)** related to the manifestation of the issue
- 📍 **Location of the affected source code** (tag/branch/commit or direct URL)
- ⚙️ **Special configuration** required to reproduce the issue
- 🔄 **Step-by-step instructions** to reproduce the issue
- 💥 **Proof-of-concept or exploit code** (if possible)
- 🎯 **Impact of the issue**, including how an attacker might exploit the issue

## 📞 Response Timeline

- **Initial Response**: Within 48 hours of receiving your report
- **Status Update**: Within 7 days with a more detailed response
- **Resolution**: We aim to resolve critical issues within 30 days

## 🏆 Recognition

We believe in acknowledging security researchers who help improve our security:

- 📝 **Security Advisory**: We will credit you in the security advisory (unless you prefer to remain anonymous)
- 🎖️ **Hall of Fame**: Recognition in our security contributors list

## 🔐 Security Best Practices

### For Users

- 🔄 **Keep Updated**: Always use the latest version of the Docker images
- 🔑 **Network Security**: Run containers on isolated networks when possible
- 🌐 **Local Use Only**: These emulators are designed for local development only
- 📱 **Environment Security**: Keep your Docker environment and host system updated

### For Developers

- 🛡️ **Container Security**: Use official Microsoft images for Azure service emulators
- 🔒 **Network Isolation**: Configure proper network segmentation
- 📊 **Monitoring**: Monitor container logs for unusual activity
- 🔄 **Updates**: Keep Docker images updated via Dependabot

## 📚 Additional Resources

- [Docker Security Best Practices](https://docs.docker.com/develop/security-best-practices/)
- [Azure Security Documentation](https://docs.microsoft.com/en-us/azure/security/)
 
## 📋 Security Checklist

Our security measures include:

- ✅ **Official Images**: Using only official Microsoft Azure emulator images
- ✅ **Network Isolation**: Containers run on isolated Docker networks
- ✅ **Local Development**: Services designed for local development environments only
- ✅ **Dependency Scanning**: Automated via Dependabot
- ✅ **Regular Updates**: Keeping emulator images current
- ✅ **Documentation**: Clear security guidelines and best practices

---

**Thank you for helping keep Azure Stack and our users safe! 🔵**