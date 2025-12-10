```cpp
// Constants
const int kMaxConnections = 100;
const std::string kDefaultHost = "localhost";

class DatabaseConnection {
 private:
  // Member variables with trailing underscore
  std::string host_name_;
  int port_;
  static int active_connections_;  // Static, no special prefix
  
 public:
  // Constructor - parameters have no prefix
  DatabaseConnection(const std::string& host_name, int port)
      : host_name_(host_name), port_(port) {
    active_connections_++;
  }
  
  // Methods are PascalCase
  bool Connect() {
    int retry_count = 0;  // Local variable
    // ...
    return true;
  }
  
  // Getters/Setters
  const std::string& host_name() const { return host_name_; }
  void set_host_name(const std::string& host_name) { host_name_ = host_name; }
};

// Global (avoided when possible, but if needed)
extern DatabaseConnection* g_primary_connection;
```