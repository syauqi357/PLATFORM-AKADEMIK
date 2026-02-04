# Usage

Learn how to use Platform Akademik effectively.

## Basic Example

Import and use components in your Svelte files:

```svelte
<script>
  import { Button, Card, Input } from '$lib/components';
  import { courseStore } from '$lib/stores';

  let searchQuery = '';
</script>

<Card>
  <Input
    bind:value={searchQuery}
    placeholder="Search courses..."
  />
  <Button on:click={() => courseStore.search(searchQuery)}>
    Search
  </Button>
</Card>
```

## Working with Courses

### Fetching Courses

```javascript
import { getCourses } from '$lib/api';

const courses = await getCourses({
  page: 1,
  limit: 10,
  status: 'active'
});
```

### Creating a Course

```javascript
import { createCourse } from '$lib/api';

const newCourse = await createCourse({
  name: 'Introduction to Programming',
  code: 'CS101',
  credits: 3,
  semester: '2025/2026 Ganjil'
});
```

## Working with Students

### Enrollment

```javascript
import { enrollStudent } from '$lib/api';

await enrollStudent({
  courseId: 'crs_12345',
  studentId: 'std_67890'
});
```

### Grade Submission

```javascript
import { submitGrade } from '$lib/api';

await submitGrade({
  courseId: 'crs_12345',
  studentId: 'std_67890',
  component: 'midterm',
  score: 85
});
```

## Using Stores

Platform Akademik uses Svelte stores for state management:

```javascript
import { writable } from 'svelte/store';

// User store
export const user = writable(null);

// Course store
export const courses = writable([]);

// UI state
export const isLoading = writable(false);
```

## Event Handling

```svelte
<script>
  function handleSubmit(event) {
    event.preventDefault();
    // Handle form submission
  }

  function handleError(error) {
    console.error('An error occurred:', error);
    // Show error notification
  }
</script>
```

> **Warning:** This platform is currently in beta. Some features may change in future releases.

## Best Practices

1. **Always handle errors** - Wrap API calls in try-catch blocks
2. **Use TypeScript** - For better type safety and IDE support
3. **Follow naming conventions** - Use camelCase for variables, PascalCase for components
4. **Keep components small** - Split large components into smaller, reusable pieces
