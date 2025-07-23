# 🚀 Chinook Workshop Setup Guide

Welcome to your pre-flight checklist! ✈️ Let's get your development environment ready for the 7-day adventure ahead.

## 📋 Prerequisites Checklist

Before diving into Day 1, make sure you have these tools installed and ready:

### ✅ Core Requirements

#### 1. 🐹 Go (Latest Version)
```bash
# Check if Go is installed
go version

# Should show Go 1.21+ (latest stable)
# If not installed, download from: https://golang.org/dl/
```

**Mac Installation (Recommended):**
```bash
# Using Homebrew (easiest)
brew install go

# Or download installer from golang.org
```

#### 2. 🛠️ Buf CLI (The Star of the Show!)
```bash
# Install Buf CLI on Mac
brew install bufbuild/buf/buf

# Verify installation
buf --version

# Should show buf version 1.28.0+ or later
```

#### 3. 🐘 SQLite (Local Database)

If you're on a Mac (which you are if you work at Buf) you have SQLite3 installed. If you're on Windows, [here you go](https://www.sqlite.org/download.html). Make sure the SQLite3 binary (`sqlite3`) is in your path.

#### 4. ☁️ AWS CLI (For S3 Integration)
```bash
# Install AWS CLI
brew install awscli

# Configure with dummy credentials for local testing
aws configure
# Use fake keys for local development:
# AWS Access Key ID: test
# AWS Secret Access Key: test
# Default region: us-east-1
# Default output format: json
```

### 🔧 Development Tools (Recommended)

#### Code Editor Setup
- **VS Code** with Go and Protobuf extensions:
  ```bash
  # Install VS Code extensions
  code --install-extension golang.go
  code --install-extension bufbuild.vscode-buf
  ```

#### Additional Utilities
```bash
# Install useful tools
brew install jq          # JSON processing
brew install httpie      # API testing
brew install docker      # For advanced scenarios
```

## 🧪 Environment Verification

Run this verification script to ensure everything is working:

```bash
# Create verification script
cat > verify_setup.sh << 'EOF'
#!/bin/bash
echo "🚀 Chinook Setup Verification"
echo "================================"

# Check Go
echo -n "Go: "
if command -v go &> /dev/null; then
    go version
else
    echo "❌ NOT INSTALLED"
fi

# Check Buf
echo -n "Buf CLI: "
if command -v buf &> /dev/null; then
    buf --version
else
    echo "❌ NOT INSTALLED"
fi

# Check SQLite
echo -n "SQLite: "
if command -v sqlite3 &> /dev/null; then
    sqlite3 -version
else
    echo "❌ NOT INSTALLED"
fi

# Check AWS CLI
echo -n "AWS CLI: "
if command -v aws &> /dev/null; then
    aws --version
else
    echo "❌ NOT INSTALLED"
fi

# Test database connection
echo -n "Database Connection: "
if sqlite3 ../resources/chinook.db "SELECT 1;" &> /dev/null; then
    echo "✅ CONNECTED"
else
    echo "❌ CANNOT CONNECT"
fi

echo ""
echo "🎯 Setup Status:"
echo "If all items show ✅, you're ready for Day 1!"
echo "If any show ❌, install the missing tools above."
EOF

# Make it executable and run
chmod +x verify_setup.sh
./verify_setup.sh
```

## 📁 Project Structure Setup

Create your workshop workspace:

```bash
# Navigate to your protobuf directory
cd /Users/rob/@Sync/bufstuff/protobuf

# Initialize Go module for the entire workshop
go mod init example.com/chinook/workshop

# Create workspace structure
mkdir -p {cmd,internal,pkg,data,scripts}

# Set up Git (optional but recommended)
git init
echo "# Chinook Workshop" > README.md
echo "vendor/" > .gitignore
echo "*.log" >> .gitignore
echo ".env" >> .gitignore
```

## 🎯 Quick Test: Your First Protobuf!

Let's make sure everything works with a quick test:

```bash
# Create a simple test proto
mkdir -p proto/test
cat > proto/test/hello.proto << 'EOF'
syntax = "proto3";

package test.v1;

option go_package = "example.com/chinook/workshop/internal/proto/test/v1;testv1";

message HelloRequest {
  string name = 1;
}

message HelloResponse {
  string message = 1;
}

service HelloService {
  rpc SayHello(HelloRequest) returns (HelloResponse);
}
EOF

# Create buf configuration
cat > buf.yaml << 'EOF'
version: v1
breaking:
  use:
    - FILE
lint:
  use:
    - DEFAULT
EOF

# Create buf generate configuration
cat > buf.gen.yaml << 'EOF'
version: v1
plugins:
  - plugin: buf.build/protocolbuffers/go
    out: internal/proto
    opt: paths=source_relative
  - plugin: buf.build/grpc/go
    out: internal/proto
    opt: paths=source_relative
EOF

# Generate Go code
buf generate proto/test

# If this works without errors, you're ready! 🎉
```

## 🆘 Troubleshooting Common Issues

### Go Module Issues
```bash
# If you get module errors:
go mod tidy
go mod download
```

### Buf CLI Issues
```bash
# If buf commands fail:
buf mod update
buf build  # Should complete without errors
```

### Path Issues
```bash
# Add to your ~/.zshrc or ~/.bash_profile:
export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:$(go env GOPATH)/bin
```

## 🎉 You're Ready!

If your verification script shows all ✅, you're ready to start Day 1! 

Your adventure begins with:
```bash
cd day01-foundation
cat LECTURE.md
```

**Pro Tip**: Keep this SETUP.md handy - you might need to reference it during the workshop if you encounter environment issues.

Happy coding! 🚀✨

---
*"A well-prepared developer is a confident developer!"* 💪