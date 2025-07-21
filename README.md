# 🎯 The Chinook Workshop: 7 Days of Buf + Go Magic! ✨

Welcome to your epic journey from zero to Buf hero! 🚀 Over the next 7 days, you'll build a complete data pipeline for Chinook using Go, Protobuf, and Bufstream. No boring theory - just hands-on, break-things-and-fix-them learning! 🔥

You'll also learn Go, Protobuf, and BufStream along the way. This workshop teaches Go, Protobuf, and BufStream through a real-world scenario: streaming data from a SQLite3 database to S3 using BufStream. No prior knowledge assumed.

You'll encounter intentional errors - this is by design.

## 📚 Learning By Failure

This workshop uses deliberate obstacles to deepen understanding. Some examples contain intentional issues for you to discover and fix. Use any tools (including AI) to problem-solve.

## 📝 Track Your Progress

- Complete one session per day maximum
- Log fixes and learnings in code comments or `JOURNAL.md`
- Write code by hand when possible for better retention
- Copy/paste is acceptable, but manual typing builds muscle memory

## 🚀 Getting Started

1. Follow `SETUP.md` for installation
2. Work through sessions sequentially
3. Take time to reflect between sessions
4. Document your journey

## 🏢 The Chinook Story
You're the new data architect at Chinook, a growing company that needs to move customer data from their Postgres database to S3 for analytics. Your mission: build a bulletproof data pipeline using modern tools! 

## 📅 Your 7-Day Adventure

### Day 1: 🛠️ "Foundation Day" - Setting Up Your Arsenal
**Topic**: Go Project Structure & Buf CLI Setup
- Install and configure Buf CLI 
- Set up your Go workspace with proper idioms
- Create your first .proto schema
- **Labs**: 5 hands-on exercises building your project skeleton
- **Pitfall Focus**: Go module management and GOPATH confusion

### Day 2: 🎯 "Schema Master" - Protobuf Deep Dive  
**Topic**: Advanced Protobuf Design & Code Generation
- Schema evolution strategies
- Backwards compatibility nightmares (and solutions!)
- Go-specific protobuf patterns
- **Labs**: 4 exercises designing Chinook's customer schema
- **Pitfall Focus**: Breaking changes and field numbering disasters

### Day 3: 🏗️ "Builder Day" - Go Service Architecture
**Topic**: Idiomatic Go Service Design
- Error handling the Go way (no more exceptions!)
- Interface design patterns
- Dependency injection without frameworks
- **Labs**: 5 exercises building your data service layer
- **Pitfall Focus**: Pointer vs value receivers and nil panics

### Day 4: 🔌 "Connection Day" - Database Integration
**Topic**: Postgres + Go + Protobuf Integration
- Database connection patterns
- Scanning rows into protobuf messages
- Transaction handling idioms
- **Labs**: 4 exercises connecting to your Chinook database
- **Pitfall Focus**: SQL injection and connection leaks

### Day 5: 🌊 "Stream Day" - Bufstream Introduction
**Topic**: Event Streaming with Bufstream
- Producer/consumer patterns
- Message serialization strategies
- Error handling in distributed systems
- **Labs**: 5 exercises setting up your data stream
- **Pitfall Focus**: Message ordering and delivery guarantees

### Day 6: ☁️ "Cloud Day" - S3 Integration & Deployment
**Topic**: AWS S3 Integration & Production Patterns
- S3 client patterns in Go
- Batch processing strategies
- Monitoring and observability
- **Labs**: 4 exercises deploying your pipeline
- **Pitfall Focus**: Credential management and rate limiting

### Day 7: 🎉 "Victory Day" - Testing & Advanced Patterns
**Topic**: Testing Strategies & Performance Optimization
- Unit testing with mocks
- Integration testing patterns
- Performance profiling
- **Labs**: 4 exercises ensuring your pipeline is bulletproof
- **Pitfall Focus**: Race conditions and memory leaks

## 🎯 Learning Philosophy

### The "Fail Fast, Learn Faster" Approach 💥
- Each day includes deliberate failure scenarios
- You'll break things, then fix them (the best way to learn!)
- Real-world edge cases, not toy examples
- Solutions provided, but try first!

### Go Idioms You'll Master 🐹
- Error handling without exceptions
- Interface-driven design
- Goroutine patterns and channel communication
- Memory management and garbage collection awareness
- The "Go way" of structuring projects

### Protobuf Mastery 📦
- Schema design best practices
- Evolution strategies that won't break production
- Performance optimization techniques
- Cross-language compatibility considerations

## 🎮 Each Lab Includes:
- **🎯 Objectives**: What you'll accomplish
- **🛠️ Step-by-step instructions** with real code
- **💥 Deliberate failure points** to test your understanding  
- **🔍 Further Exploration** for going deeper
- **🚨 Common Pitfalls** section with solutions
- **✅ Victory Conditions** so you know you succeeded

## 🏆 Final Project
By day 7, you'll have built a complete, production-ready data pipeline that:
- ✅ Reads customer data from Postgres
- ✅ Converts to protobuf messages
- ✅ Streams through Bufstream
- ✅ Lands in S3 as structured data
- ✅ Includes monitoring, error handling, and tests
- ✅ Follows Go and Protobuf best practices

Ready to become a Buf + Go wizard? Let's dive in! 🧙‍♂️✨

---
*"The best way to learn is to build something real, break it, then make it better!"* 🔥