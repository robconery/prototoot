# Day 4: = Connection Day - Database Integration

Connect your Go services to the real world! Today you'll integrate with SQLite, implement proper data patterns, and store protobuf data efficiently.

## 🎯 Today's Mission
- Connect Go services to SQLite using the Chinook database
- Store and query protobuf data efficiently  
- Implement repository patterns with transactions
- Build database migration and health monitoring

## 🐘 Database Design Philosophy

### Protobuf + SQLite Strategy
```sql
-- Hybrid approach: structured + flexible with existing Chinook data
-- Extend existing customers table
ALTER TABLE customers ADD COLUMN status INTEGER DEFAULT 1;
ALTER TABLE customers ADD COLUMN data TEXT; -- JSON as TEXT in SQLite
ALTER TABLE customers ADD COLUMN created_at DATETIME DEFAULT CURRENT_TIMESTAMP;
ALTER TABLE customers ADD COLUMN updated_at DATETIME DEFAULT CURRENT_TIMESTAMP;

-- Indexes for performance
CREATE INDEX idx_customers_email ON customers(email);
CREATE INDEX idx_customers_status ON customers(status);
CREATE INDEX idx_customers_phone ON customers(phone);
-- Note: SQLite doesn't have GIN indexes, but JSON operations still work
```

### Connection Management
```go
// SQLite connection with proper configuration
func NewDatabase(cfg DatabaseConfig) (*sql.DB, error) {
    dsn := fmt.Sprintf("file:%s?cache=shared&mode=rwc", cfg.DatabasePath)
    db, err := sql.Open("sqlite3", dsn)
    if err != nil {
        return nil, err
    }
    
    // Configure for SQLite
    db.SetMaxOpenConns(1) // SQLite only allows one writer
    db.SetMaxIdleConns(1)
    db.SetConnMaxLifetime(cfg.ConnMaxLifetime)
    
    // Enable WAL mode for better concurrency
    _, err = db.Exec("PRAGMA journal_mode=WAL; PRAGMA foreign_keys=ON;")
    
    return db, nil
}
```

## 🎯 Today's Lab Overview

### Lab 1: 🐘 SQLite Integration
- Connect to existing Chinook SQLite database
- Extend database schema for protobuf storage
- Implement connection management and health checks

### Lab 2: = Repository Pattern Implementation
- Build repository layer with proper abstractions
- Implement CRUD operations with transactions
- Handle database errors gracefully

### Lab 3: 🐘 Query Optimization & Performance
- Design efficient queries for protobuf data
- Implement caching strategies
- Build connection monitoring

### Lab 4: 🧪 Database Testing Strategies
- Set up test databases with containers
- Create fixtures and migration testing
- Build integration test suites

Ready to connect to the real world? Let's build! 🐘