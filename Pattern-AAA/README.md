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
  
  height: 110px;  }
  
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

# **Pattern AAA (Arrange-Act-Assert)**
### Testing Standard

**Created by :** <span class="highlight">Aziz Soufiane</span>  
**Supervised by :** <span class="highlight">M. ESSARRAJ Fouad</span>  
**Program :** Full-Stack Web Developer

---

## 🧐 What is the AAA Pattern?

The **AAA** pattern is a convention for organizing unit tests that divides the test into three distinct logical blocks.

<div class="dt-card">
  <h4>Main objectives:</h4>
  <ul>
    <li>Separate preparation from execution.</li>
    <li>Improve code readability.</li>
    <li>Facilitate debugging (know exactly where it fails).</li>
  </ul>
</div>

---

## 🛠️ 1. Arrange (Setup)

This is the configuration step. We prepare everything needed to run the test.

- **Actions:** Variable initialization, Model creation (Factories), Mocks configuration.
- **Question:** *What do I need to execute this test?*

> [!NOTE]
> This is generally the longest part of the test.

---

## ⚡ 2. Act (Execution)

This is the step where we call the method or functionality we want to test.

- **Actions:** Function execution, API endpoint call.
- **Rule:** Ideally, this step should contain only **one line** of code.
- **Question:** *What is the action I'm testing?*

---

## ✅ 3. Assert (Verification)

The final step where we verify if the obtained result matches the expected result.

- **Actions:** HTTP status verification, database verification, value comparison.
- **Question:** *Is the behavior correct?*

---

## 🚀 Concrete Example: Laravel

<div style="font-size: 0.85em;">

```php
public function test_user_can_publish_post()
{
    // --- ARRANGE ---
    $user = User::factory()->create();
    $postData = ['title' => 'My Post', 'body' => 'Content...'];

    // --- ACT ---
    $response = $this->actingAs($user)->post('/posts', $postData);

    // --- ASSERT ---
    $response->assertStatus(201);
    $this->assertDatabaseHas('posts', ['title' => 'My Post']);
}