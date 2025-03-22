# Development Architecture

## Development Workflow

### 1. Issue-First Development
Every feature begins with a GitHub issue that includes:
- Feature description
- Acceptance criteria
- Technical requirements
- UI/UX considerations
- Testing requirements

### 2. Branch Management
- Branch naming convention: `feature/[issue-number]-[brief-description]`
- All development work happens in feature branches
- Pull requests are required for merging into main
- Code review process must be completed before merge

### 3. UI Development Process
#### Storybook-First Approach
- All UI components are developed and tested in Storybook
- Components must have:
  - Documentation
  - Props interface
  - Usage examples
  - Different states/variants
  - Responsive behavior demonstrations
- Storybook approval required before Next.js implementation

### 4. Technical Stack

#### Frontend
- **Framework**: Next.js
  - App Router for routing
  - Server Components for improved performance
  - Server Actions for data mutations
  - React Server Components for optimal rendering strategy

- **UI Development**
  - Storybook for component development
  - Tailwind CSS for styling
  - Shadcn/ui for base components
  - TypeScript for type safety

#### Backend Integration
- **Supabase**
  - PostgreSQL database
  - Real-time subscriptions for live updates
  - Row Level Security (RLS) for data protection
  - Authentication and Authorization
  - Storage for assets

### 5. Code Architecture

#### Service Layer Pattern
```typescript
// Example service structure
class UserService {
  constructor(private readonly db: SupabaseClient) {}

  async findOne(id: string): Promise<User> {
    // Implementation
  }

  async create(data: CreateUserDto): Promise<User> {
    // Implementation
  }

  async update(id: string, data: UpdateUserDto): Promise<User> {
    // Implementation
  }
}
```

#### Server Actions Integration
```typescript
// Example server action with service
export async function createUser(formData: FormData) {
  'use server'
  
  const userService = new UserService(supabase)
  const data = Object.fromEntries(formData)
  
  return await userService.create(data)
}
```

#### Real-time Updates
```typescript
// Example real-time subscription
const useUsers = () => {
  const [users, setUsers] = useState<User[]>([])

  useEffect(() => {
    const channel = supabase
      .channel('users')
      .on('postgres_changes', 
          { event: '*', schema: 'public', table: 'users' },
          (payload) => {
        // Handle real-time updates
      })
      .subscribe()

    return () => {
      supabase.removeChannel(channel)
    }
  }, [])

  return users
}
```

### 6. Directory Structure
```
src/
├── app/                    # Next.js app router pages
├── components/            
│   ├── ui/                # Reusable UI components
│   └── features/          # Feature-specific components
├── services/              # Business logic services
├── lib/                   # Utility functions and configurations
├── types/                 # TypeScript type definitions
├── stories/               # Storybook stories
└── styles/                # Global styles and Tailwind config
```

### 7. Testing Strategy
- Unit tests for services
- Component tests in Storybook
- Integration tests for server actions
- E2E tests for critical user flows

### 8. Quality Assurance
- ESLint for code quality
- Prettier for code formatting
- Husky for pre-commit hooks
- GitHub Actions for CI/CD
- Automated testing in pipeline
- Storybook visual regression testing

### 9. Deployment
- Vercel for Next.js deployment
- Supabase Cloud for backend services
- Automated deployments via GitHub Actions
- Preview deployments for pull requests

This architecture emphasizes:
- Component-driven development
- Type safety
- Real-time capabilities
- Service-oriented backend logic
- Automated testing and quality assurance
- Scalable and maintainable code structure 