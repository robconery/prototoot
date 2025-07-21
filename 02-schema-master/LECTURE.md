# Day 2: 🎯 Schema Master - Protobuf Deep Dive

Welcome to Schema Evolution Hell (and how to escape it)! = Today you'll master advanced protobuf design patterns and learn how to evolve schemas without breaking production systems.

## 🎯 Today's Mission
By the end of today, you'll have:
- Mastered protobuf schema evolution strategies
- Built backwards-compatible API versions
- Implemented field deprecation and migration patterns
- Created a schema registry system
- Survived deliberate breaking changes (and fixed them!)

## 🔥 Schema Evolution: The Good, The Bad, The Ugly

### The Protobuf Promise >
Protobuf's superpower is **backwards compatibility**. But with great power comes great responsibility!

### Safe Changes (The Good) 
```protobuf
// Adding new fields (always safe)
message Customer {
  int64 id = 1;
  string name = 2;
  string email = 3;
  string phone = 4;        //  NEW FIELD - Safe!
  repeated Tag tags = 5;   //  NEW REPEATED - Safe!
}

// Adding new enum values (usually safe)
enum Status {
  STATUS_UNSPECIFIED = 0;
  STATUS_ACTIVE = 1;
  STATUS_INACTIVE = 2;
  STATUS_SUSPENDED = 3;    //  NEW VALUE - Safe!
}
```

### Dangerous Changes (The Bad) ⚠️
```protobuf
// Changing field types - DANGER!
message Customer {
  string id = 1;           // ⚠️ Was int64 - Risky!
  int32 phone = 4;         // ⚠️ Was string - Risky!
}

// Renaming fields - DANGER!
message Customer {
  int64 customer_id = 1;   // ⚠️ Was 'id' - Risky!
}
```

### Breaking Changes (The Ugly) L
```protobuf
// Reusing field numbers - NEVER DO THIS!
message Customer {
  int64 id = 1;
  string name = 2;
  // string email = 3;     // L DELETED
  string address = 3;      // L REUSED NUMBER 3!
}

// Removing required fields - INSTANT BREAKAGE!
message Customer {
  int64 id = 1;
  // required string name = 2;  // L REMOVED REQUIRED!
}
```

## = Schema Evolution Strategies

### Strategy 1: Additive Evolution
Always add, never remove or change:
```protobuf
// v1
message Customer {
  int64 id = 1;
  string name = 2;
}

// v2 - Add fields
message Customer {
  int64 id = 1;
  string name = 2;
  string email = 3;        // Added
  repeated Address addresses = 4;  // Added
}
```

### Strategy 2: Deprecation Pattern
Mark fields as deprecated before removing:
```protobuf
message Customer {
  int64 id = 1;
  string name = 2;
  string old_phone = 3 [deprecated = true];  // Mark deprecated
  ContactInfo contact = 4;                   // New way
}
```

### Strategy 3: Oneof Evolution
Use oneof for polymorphic data:
```protobuf
message PaymentMethod {
  oneof method {
    CreditCard credit_card = 1;
    BankAccount bank_account = 2;
    DigitalWallet digital_wallet = 3;  // Can add new payment types!
  }
}
```

### Strategy 4: Versioned Services
Create new service versions for major changes:
```protobuf
// customer/v1/customer.proto
service CustomerServiceV1 {
  rpc GetCustomer(GetCustomerRequest) returns (GetCustomerResponse);
}

// customer/v2/customer.proto  
service CustomerServiceV2 {
  rpc GetCustomer(GetCustomerRequestV2) returns (GetCustomerResponseV2);
  rpc SearchCustomers(SearchRequest) returns (SearchResponse);  // New!
}
```

## 📱 Common Pitfalls (Today's Failure Scenarios!)

### Pitfall 1: Field Number Reuse 📱
**The Crime**: Reusing field numbers
**The Consequence**: Silent data corruption
**The Fix**: Never reuse numbers, mark as reserved

### Pitfall 2: Type Changes =%
**The Crime**: Changing int64 to string
**The Consequence**: Deserialization failures
**The Fix**: Add new field, deprecate old

### Pitfall 3: Required Field Removal ⚠️
**The Crime**: Removing required fields
**The Consequence**: Instant breakage across services
**The Fix**: Deprecate first, remove after migration

### Pitfall 4: Enum Zero Value Changes <*
**The Crime**: Changing what enum value 0 means
**The Consequence**: Default behavior changes
**The Fix**: Never change zero value semantics

## 🔥 Today's Lab Preview

### Lab 1: = Schema Evolution Simulator
- Start with a simple schema
- Evolve it through multiple versions
- Break it deliberately, then fix it
- Learn the safe evolution patterns

### Lab 2: 📱 Multi-Version API Support
- Support both v1 and v2 customers
- Build adapters between versions
- Handle migration scenarios
- Test backwards compatibility

### Lab 3: 📱 Field Deprecation & Migration
- Deprecate old fields properly
- Migrate data to new structures
- Handle mixed version deployments
- Create migration tooling

### Lab 4: 🎯 Advanced Schema Patterns
- Implement polymorphic data with oneof
- Create extensible message designs
- Use Any types for dynamic content
- Build plugin-style architectures

## 📱 Pro Tips for Schema Design

### 1. Plan for Growth 📱
```protobuf
message Customer {
  int64 id = 1;
  string name = 2;
  string email = 3;
  
  // Reserve field numbers for future use
  reserved 4 to 10;
  reserved "old_field_name";
  
  // Use higher numbers for less common fields
  map<string, string> metadata = 50;
}
```

### 2. Use Semantic Versioning 🎯
```protobuf
// File naming convention
// customer/v1/customer.proto
// customer/v2/customer.proto

// Package naming
package customer.v1;
package customer.v2;
```

### 3. Document Breaking Changes 📱
```protobuf
// BREAKING CHANGE v2.0.0:
// - Removed deprecated 'phone' field (use contact.phone instead)
// - Changed 'status' enum values (INACTIVE split into SUSPENDED/DORMANT)
message Customer {
  // ... 
}
```

### 4. Test Compatibility 🔥
```go
// Always test that old clients can read new data
func TestBackwardsCompatibility(t *testing.T) {
  // Create message with v2 schema
  newCustomer := &customerv2.Customer{...}
  
  // Serialize with v2
  data, _ := proto.Marshal(newCustomer)
  
  // Deserialize with v1 - should work!
  var oldCustomer customerv1.Customer
  err := proto.Unmarshal(data, &oldCustomer)
  // Should not error!
}
```

## 🎯 Success Metrics
By day's end, you'll confidently:
-  Evolve schemas without breaking existing clients
-  Handle mixed-version deployments
-  Migrate data between schema versions
-  Design extensible, future-proof schemas
-  Avoid the most common schema evolution disasters

## 📱 Ready to Become a Schema Master?

Head to `lab01/` and let's start evolving! Remember:

> *"Schema evolution is like brain surgery - you can do it successfully, but you better know what you're doing!"* 🔥

Let's master the art of schema evolution! 🎯

---

**Pro Tip**: Keep the protobuf language guide open: https://protobuf.dev/programming-guides/ - it's your schema evolution bible! 📱