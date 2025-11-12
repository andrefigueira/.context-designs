# State Management with Alpine.js

## State Philosophy

State management in templates should be simple, declarative, and scoped to components. Alpine.js provides reactive state without the complexity of larger frameworks, making it ideal for template-based projects.

## Component-Level State

### Basic State Declaration

Initialize state with `x-data` directive:

```html
<div x-data="{ count: 0, name: '' }">
  <p x-text="count"></p>
  <button @click="count++">Increment</button>

  <input x-model="name" type="text" />
  <p>Hello, <span x-text="name"></span>!</p>
</div>
```

**Key concepts:**
- `x-data` creates isolated component scope
- State is reactive and updates DOM automatically
- Multiple state properties can coexist

### Object State

For complex components, use object-based state with methods:

```html
<div x-data="{
  form: {
    email: '',
    password: '',
    rememberMe: false
  },
  errors: {},
  isSubmitting: false,

  validateEmail() {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
    if (!emailRegex.test(this.form.email)) {
      this.errors.email = 'Please enter a valid email address'
      return false
    }
    delete this.errors.email
    return true
  },

  async submitForm() {
    if (!this.validateEmail()) return

    this.isSubmitting = true
    try {
      // Simulate API call
      await fetch('/api/login', {
        method: 'POST',
        body: JSON.stringify(this.form)
      })
      alert('Login successful!')
    } catch (error) {
      this.errors.general = 'Login failed. Please try again.'
    } finally {
      this.isSubmitting = false
    }
  }
}">
  <form @submit.prevent="submitForm" class="space-y-4">
    <!-- Email input -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">
        Email
      </label>
      <input x-model="form.email"
             @blur="validateEmail"
             type="email"
             :class="errors.email ? 'border-red-500' : 'border-gray-300'"
             class="w-full px-4 py-2 border rounded-lg">
      <p x-show="errors.email" x-text="errors.email" class="text-sm text-red-600 mt-1"></p>
    </div>

    <!-- Password input -->
    <div>
      <label class="block text-sm font-medium text-gray-700 mb-1">
        Password
      </label>
      <input x-model="form.password"
             type="password"
             class="w-full px-4 py-2 border border-gray-300 rounded-lg">
    </div>

    <!-- Remember me checkbox -->
    <label class="flex items-center">
      <input x-model="form.rememberMe" type="checkbox" class="rounded">
      <span class="ml-2 text-sm text-gray-700">Remember me</span>
    </label>

    <!-- Submit button -->
    <button type="submit"
            :disabled="isSubmitting"
            class="w-full px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 disabled:opacity-50">
      <span x-show="!isSubmitting">Sign In</span>
      <span x-show="isSubmitting">Signing in...</span>
    </button>

    <!-- General error -->
    <p x-show="errors.general" x-text="errors.general" class="text-sm text-red-600"></p>
  </form>
</div>
```

## Data Binding

### Text Binding

```html
<div x-data="{ message: 'Hello World' }">
  <!-- Display text content -->
  <p x-text="message"></p>

  <!-- Display as HTML (use with caution) -->
  <div x-html="message"></div>
</div>
```

### Two-Way Binding

```html
<div x-data="{ search: '' }">
  <!-- Text input -->
  <input x-model="search" type="text" placeholder="Search..." />

  <!-- Checkbox -->
  <input x-model="agreed" type="checkbox" />

  <!-- Radio buttons -->
  <input x-model="plan" type="radio" value="basic" />
  <input x-model="plan" type="radio" value="premium" />

  <!-- Select dropdown -->
  <select x-model="category">
    <option value="tech">Technology</option>
    <option value="design">Design</option>
  </select>

  <!-- Show current values -->
  <pre x-text="JSON.stringify({ search, agreed, plan, category }, null, 2)"></pre>
</div>
```

### Modifiers

```html
<div x-data="{ value: '' }">
  <!-- Lazy: Update on change instead of input -->
  <input x-model.lazy="value" />

  <!-- Number: Convert string to number -->
  <input x-model.number="age" type="number" />

  <!-- Debounce: Wait 500ms after typing stops -->
  <input x-model.debounce.500ms="searchQuery" />

  <!-- Throttle: Update at most once per 1000ms -->
  <input x-model.throttle.1000ms="position" />
</div>
```

## Computed Properties

Use getters for derived state:

```html
<div x-data="{
  firstName: 'John',
  lastName: 'Doe',

  get fullName() {
    return `${this.firstName} ${this.lastName}`
  }
}">
  <input x-model="firstName" placeholder="First name" />
  <input x-model="lastName" placeholder="Last name" />

  <p>Full name: <span x-text="fullName"></span></p>
</div>
```

## Conditional Rendering

### Show/Hide with x-show

```html
<div x-data="{ showDetails: false }">
  <button @click="showDetails = !showDetails">Toggle Details</button>

  <!-- Element remains in DOM, hidden with CSS -->
  <div x-show="showDetails" x-transition>
    <p>These are the details...</p>
  </div>
</div>
```

### Conditional Rendering with x-if

```html
<div x-data="{ loggedIn: false }">
  <!-- Element added/removed from DOM -->
  <template x-if="loggedIn">
    <div class="p-4 bg-green-100 rounded">
      Welcome back!
    </div>
  </template>

  <template x-if="!loggedIn">
    <div class="p-4 bg-gray-100 rounded">
      Please sign in.
    </div>
  </template>

  <button @click="loggedIn = !loggedIn">
    Toggle Login State
  </button>
</div>
```

**Use x-show when:**
- Element toggles frequently
- Want CSS transitions
- Element is not expensive to render

**Use x-if when:**
- Element rarely changes
- Element is expensive to render
- Want complete DOM removal

## Lists and Iteration

```html
<div x-data="{
  todos: [
    { id: 1, text: 'Learn Alpine.js', completed: false },
    { id: 2, text: 'Build templates', completed: true },
    { id: 3, text: 'Launch project', completed: false }
  ],
  newTodo: '',

  addTodo() {
    if (this.newTodo.trim()) {
      this.todos.push({
        id: Date.now(),
        text: this.newTodo,
        completed: false
      })
      this.newTodo = ''
    }
  },

  toggleTodo(id) {
    const todo = this.todos.find(t => t.id === id)
    if (todo) todo.completed = !todo.completed
  },

  removeTodo(id) {
    this.todos = this.todos.filter(t => t.id !== id)
  },

  get incompleteTodos() {
    return this.todos.filter(t => !t.completed).length
  }
}">
  <!-- Add todo form -->
  <div class="flex gap-2 mb-4">
    <input x-model="newTodo"
           @keydown.enter="addTodo"
           type="text"
           placeholder="Add a todo..."
           class="flex-1 px-4 py-2 border rounded-lg" />
    <button @click="addTodo"
            class="px-4 py-2 bg-blue-600 text-white rounded-lg">
      Add
    </button>
  </div>

  <!-- Todo count -->
  <p class="text-sm text-gray-600 mb-2">
    <span x-text="incompleteTodos"></span> incomplete tasks
  </p>

  <!-- Todo list -->
  <ul class="space-y-2">
    <template x-for="todo in todos" :key="todo.id">
      <li class="flex items-center gap-3 p-3 bg-white border rounded-lg">
        <input type="checkbox"
               :checked="todo.completed"
               @click="toggleTodo(todo.id)"
               class="rounded" />

        <span :class="todo.completed ? 'line-through text-gray-500' : ''"
              class="flex-1"
              x-text="todo.text"></span>

        <button @click="removeTodo(todo.id)"
                class="text-red-600 hover:text-red-800">
          Delete
        </button>
      </li>
    </template>
  </ul>
</div>
```

**Key points:**
- Use `template` element with `x-for`
- Always include `:key` for list items
- Access item and index: `x-for="(item, index) in items"`

## Global State with Alpine.store()

For state shared across multiple components:

```html
<!-- Define global store -->
<script>
  document.addEventListener('alpine:init', () => {
    Alpine.store('cart', {
      items: [],
      total: 0,

      addItem(product) {
        this.items.push(product)
        this.total += product.price
      },

      removeItem(index) {
        const item = this.items[index]
        this.total -= item.price
        this.items.splice(index, 1)
      },

      clear() {
        this.items = []
        this.total = 0
      }
    })
  })
</script>

<!-- Component 1: Product list -->
<div x-data>
  <button @click="$store.cart.addItem({ name: 'Widget', price: 10 })"
          class="px-4 py-2 bg-blue-600 text-white rounded-lg">
    Add Widget ($10)
  </button>
</div>

<!-- Component 2: Cart display -->
<div x-data class="fixed top-4 right-4 bg-white shadow-lg rounded-lg p-4">
  <h3 class="font-semibold mb-2">Shopping Cart</h3>

  <template x-for="(item, index) in $store.cart.items" :key="index">
    <div class="flex justify-between items-center mb-2">
      <span x-text="item.name"></span>
      <button @click="$store.cart.removeItem(index)" class="text-red-600 text-sm">
        Remove
      </button>
    </div>
  </template>

  <div class="border-t pt-2 mt-2 font-semibold">
    Total: $<span x-text="$store.cart.total"></span>
  </div>

  <button @click="$store.cart.clear()"
          class="w-full mt-2 px-4 py-2 bg-gray-200 rounded-lg">
    Clear Cart
  </button>
</div>
```

## Persistence with Alpine.persist()

Save state to localStorage automatically:

```html
<!-- Requires Alpine Persist plugin -->
<script defer src="https://cdn.jsdelivr.net/npm/@alpinejs/persist@3.x.x/dist/cdn.min.js"></script>
<script defer src="https://cdn.jsdelivr.net/npm/alpinejs@3.x.x/dist/cdn.min.js"></script>

<div x-data="{
  darkMode: $persist(false).as('darkMode'),
  preferences: $persist({
    fontSize: 'medium',
    notifications: true
  }).as('userPreferences')
}">
  <!-- Dark mode toggle -->
  <button @click="darkMode = !darkMode"
          class="px-4 py-2 bg-gray-200 rounded-lg">
    <span x-show="darkMode">Light Mode</span>
    <span x-show="!darkMode">Dark Mode</span>
  </button>

  <!-- Preferences persist across page reloads -->
  <select x-model="preferences.fontSize">
    <option value="small">Small</option>
    <option value="medium">Medium</option>
    <option value="large">Large</option>
  </select>
</div>
```

## Best Practices

1. **Scope state appropriately**: Keep state at component level unless genuinely global
2. **Use methods for logic**: Extract complex logic into methods rather than inline expressions
3. **Validate inputs**: Implement validation methods for forms
4. **Handle loading states**: Track async operations with boolean flags
5. **Clear errors**: Reset error messages when appropriate
6. **Use getters for derived data**: Compute values from existing state
7. **Persist wisely**: Only persist state that should survive page reloads

These patterns cover common state management needs while keeping templates simple and maintainable.
