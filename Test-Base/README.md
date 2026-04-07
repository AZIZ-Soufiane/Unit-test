---
marp: true
theme: default
paginate: true
backgroundColor: #f5f5f5
color: #1a1a1a
style: |
  section {
    font-family: 'JetBrains Mono', monospace;
    font-size: 24px;
    border: 1px solid #27272a;
    padding: 60px 80px;
  }
  h1 { color: #1a1a1a; font-size: 2.2em; margin-top: 80px; }
  h2 { color: #0066cc; font-size: 1.8em; border-bottom: 1px solid #cccccc; padding-bottom: 10px; }
  h3 { color: #333333; }
  code { background: #e8e8e8; color: #0066cc; border: 1px solid #cccccc; border-radius: 6px; }
  blockquote { background: #f0f0f0; border-left: 4px solid #0066cc; color: #333333; padding: 10px 20px; }
  
  .logo-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    position: absolute;
    top: 30px;   
    left: 60px;
    right: 60px;
  }
  .logo-header img {
    height: 110px;
  }
  
  .dt-card {
    background: #ffffff;
    padding: 25px;
    border-radius: 10px;
    border: 1px solid #cccccc;
    border-top: 4px solid #0066cc;
    margin-top: 20px;
  }
  
  .highlight { color: #3b82f6; font-weight: bold; }
---

<div class="logo-header">
  <img src="images/ofppt-logo.png"   alt="OFPPT">
  <img src="images/solicode_tanger.png" alt="Solicode">
</div>

# **Environment & Isolation**
### Test Base Concept

**Created by :** <span class="highlight">Aziz Soufiane</span>  
**Supervised by :** <span class="highlight">M. ESSARRAJ Fouad</span>  
**Program :** Full-Stack Web Developer

---

## 🧐 What is Test Environment?

A **test environment** is the setup where tests are executed.

<div class="dt-card">
  <h4>Includes:</h4>
  <ul>
    <li>Operating system & runtime (PHP, Node.js, etc.)</li>
    <li>Database (MySQL, SQLite)</li>
    <li>Framework configuration</li>
    <li>External services (APIs, queues)</li>
  </ul>
</div>

---

## 🔒 What is Test Isolation?

**Test isolation** ensures that each test runs independently without affecting others.

<div class="dt-card">
  <h4>Main goals:</h4>
  <ul>
    <li>No shared state between tests</li>
    <li>Predictable results</li>
    <li>Easy debugging</li>
  </ul>
</div>

---

## ⚠️ Why Isolation is Important?

Without isolation, tests can become unreliable.

- ❌ Tests may pass or fail randomly
- ❌ Hidden dependencies between tests
- ❌ Difficult debugging

> [!WARNING]
> A failing test may not mean broken code — it could be a polluted environment.

---

## 🛠️ Techniques for Isolation

### 1. Database Reset

- Use transactions or migrations
- Reset DB after each test

```php
use RefreshDatabase;

class UserTest extends TestCase {
    use RefreshDatabase;
}
```

---

## 🧪 Techniques for Isolation (Cont.)

### 2. Mocking Dependencies

Replace real services with fake ones.

```php
$mock = Mockery::mock(Service::class);
$mock->shouldReceive('process')->andReturn(true);
```

---

## 🔁 Techniques for Isolation (Cont.)

### 3. Use Factories

Generate fresh data for each test.

- ✅ Avoid hardcoded data
- ✅ Ensure uniqueness

```php
$user = User::factory()->create();
```

---

## ⚙️ Environment Configuration

Use a separate environment for testing:

```
APP_ENV=testing
DB_DATABASE=test_db
CACHE_DRIVER=array
QUEUE_CONNECTION=sync
```

- No real API calls
- No production database

---

## 🚀 Example: Laravel Test Setup

```php
public function test_user_creation()
{
    // Fresh environment
    $this->refreshDatabase();

    // Create user
    $user = User::factory()->create();

    // Assert
    $this->assertDatabaseHas('users', [
        'email' => $user->email
    ]);
}
```

---

## ✅ Best Practices

<div class="dt-card">
  <ul>
    <li>Run tests in a dedicated environment</li>
    <li>Always isolate test data</li>
    <li>Mock external services</li>
    <li>Keep tests independent</li>
    <li>Clean up after each test</li>
  </ul>
</div>

---

## 🎯 Conclusion

- Environment ensures correct setup
- Isolation ensures reliable tests
- Together → Stable & maintainable testing

**Clean tests = Confident deployments 🚀**