# Formalized Specification Languages for Verified Code Generation

## The Intent Boundary and "Soul"

### Why Intent Determines Meaningful AI Assistance

When we first discussed this, the core insight was: **consciousness in humans stems from intent** - every choice ultimately serves self-preservation (physical, emotional, spiritual). AI lacks this causal chain; it executes instructions without underlying drive for self-actualization.

**This matters because:**

Human-created art feels meaningful because we know human choices served the creator's intent. When AI generates code, the question isn't whether AI touched the process - it's **whether human intent shaped meaningful decisions**.

**The hierarchy exists at multiple levels:**

```
Level 1: Strategic intent ("build a lending platform")
Level 2: Architectural intent ("use event-driven architecture")
Level 3: Design intent ("implement repository pattern for data access")
Level 4: Implementation intent ("use PostgreSQL with connection pooling")
Level 5: Mechanical details ("specific SQL query syntax")
```

**The boundary isn't fixed - it depends on your expertise:**

- **Novice**: Intent at Level 1-2, AI does 3-5 → No soul (didn't make key decisions)
- **Intermediate**: Intent at Level 2-3, AI does 4-5 → Some soul (made architectural choices)
- **Expert**: Intent at Level 1-4, AI does 5 → Full soul (made all design decisions)

**What makes delegation appropriate:**

Not just "AI did work" vs "human did work," but: **Did human intent drive decisions at abstraction levels that matter for this system?**

If you're building a generic CRUD app, Level 3 intent might be sufficient (repository pattern, REST API, standard validation). The specific SQL queries and error messages don't carry the "soul" of the system.

If you're building a novel distributed consensus algorithm, you need intent down to Level 4 or 5 - the specific implementation details ARE the innovation.

**This reframes the entire specification approach:**

We're not trying to minimize how much you write (though that's a side benefit). We're trying to **capture intent at the right abstraction level** so that:

1. Human decisions shape the meaningful aspects of the system
2. Generated implementation follows from those decisions
3. The code reflects human architectural choices, not arbitrary AI defaults

**The verification question becomes:**

Not "is the code correct?" but "does the implementation reflect my intent?"

Structural verification helps: if you specified repository pattern and got factory pattern, that's detectable even if both compile. The **structure of the generated code** should match the **structure of your intent**.

## The Crisis: Making the Black Box Transparent

### The Dangerous Trajectory

**The current path looks like this:**

```
Natural Language → [BLACK BOX LLM] → Generated Code
```

The discourse says: "Eventually the black box will be so good we won't need to understand what's inside. AI will gather requirements, write specs, generate code, test itself, and deploy. Humans just describe what they want."

**This is presented as inevitable progress. It's actually a crisis of human agency.**

### What Happens Inside the Black Box

When you say "build a user authentication system," the LLM's internal reasoning includes:

- **Architectural choices**: Stateless JWT vs stateful sessions, OAuth2 vs simple username/password
- **Security tradeoffs**: bcrypt vs argon2, token expiration policies, refresh token rotation
- **Error handling patterns**: Exceptions vs Result types, retry logic, failure modes
- **Data modeling**: User schema, session storage, credential management
- **Integration patterns**: Middleware vs service layer, dependency injection strategy

**None of this is visible to you.** The LLM made all these decisions based on its training distribution - what's common in its training data, not what's right for your system.

**You get code that works, but embodies someone else's (the AI's) architectural philosophy.**

### Why "AI Handles Everything" Is Wrong

**1. Natural language is fundamentally ambiguous**

"Build authentication" could mean:
- OAuth2 + JWT + refresh tokens + MFA
- Simple username/password with bcrypt
- SSO integration with corporate directory
- Magic link email authentication
- Biometric authentication

AI must make arbitrary choices. Those choices define your system's architecture, and you have no visibility into why it chose what it did.

**2. Requirements emerge through implementation**

You don't know what you want until you see it. The back-and-forth between "what I asked for" and "what I actually need" is where design happens.

If that dialogue happens inside the LLM black box, **you're not designing** - you're guessing and iterating through natural language until something acceptable emerges.

**3. Verification without understanding is impossible**

"The code works" ≠ "The code is correct"

Without intermediate representations you can reason about, you can only test outcomes, not verify properties. You're in eternal QA mode, finding bugs by accident rather than preventing them by design.

**4. Maintenance requires understanding**

When something breaks (and it will), you need to understand:
- What was the intended behavior?
- What are the system's invariants?
- What assumptions were made?
- Where is the mismatch?

If all that's buried in "the AI wrote it," you're helpless. You must re-prompt and hope the AI fixes it correctly.

**5. Innovation requires understanding abstraction**

If you can't see or understand the abstractions the system uses, you can't improve them. Progress becomes "use newer AI model" rather than "develop better understanding of problem domain."

## The Alternative: Intermediate Representations as Human-in-the-Loop

### The Core Insight

**Intermediate representations at different abstraction levels are not just "specifications for the AI" - they are artifacts of human reasoning made explicit.**

What you're really doing is **making the LLM's latent space reasoning explicit and human-controllable** through layered specifications.

**The proposed architecture:**

```
Natural Language Intent
    ↓ [Human formalizes business rules]
Formal Domain Model (Alloy) ← Human-readable, machine-verifiable
    ↓ [Human verifies properties hold]
Structural Specification (Pseudocode) ← Human-readable, structurally verifiable
    ↓ [Human designs control flow]
[LLM Generation with constraints] ← Bounded by above layers
    ↓ [Human verifies structure]
Implementation Code ← Verifiable against specs
```

**Each layer captures a different kind of intent:**

**Layer 1: Business Intent (Natural Language)**
```
"Users should be able to transfer money between accounts"
```

**Layer 2: Domain Model (Alloy - Formal Properties)**
```alloy
sig Account { balance: Money }
pred transfer[from, from', to, to': Account, amount: Money] { 
    // Formal properties that MUST hold
    from.balance' = from.balance - amount
    to.balance' = to.balance + amount
    // Total balance preserved
    (from.balance + to.balance) = (from'.balance + to'.balance)
}
```

**Layer 3: Architectural Intent (Structural Specification)**
```
service PaymentService {
    pattern: transaction_script
    isolation: serializable
    flow: [load_accounts, validate_balance, deduct, add, commit]
    error_handling: rollback_on_failure
}
```

**Layer 4: Implementation (Constrained Generation)**
```
LLM generates Go code satisfying:
- Domain invariants from Layer 2 (verified by Alloy)
- Architectural structure from Layer 3 (verified by AST analysis)
- Idiomatic Go patterns
```

**Layer 5: Executable Code**
```go
func (s *PaymentService) Transfer(from, to Account, amount Money) error {
    // Generated implementation that satisfies all constraints
}
```

**At each layer, human reasoning is captured in a form that:**
- Can be inspected and understood by humans
- Can be verified (formally or structurally) by tools
- Serves as living documentation
- Constrains the layer below
- Can be modified independently

### What This Really Means

**You're not just "specifying what you want for the AI to generate."**

**You're externalizing your reasoning process into verifiable artifacts at multiple abstraction levels.**

The Alloy model isn't "input to an AI system" - it's **your understanding of the domain formalized** in a way that can be checked for logical consistency by a theorem prover.

The structural specification isn't "constraints for generation" - it's **your architectural decisions made explicit** in a way that can be verified against implementation through static analysis.

**The intermediate representations ARE your design process made manifest,** not just input to someone else's (the AI's) design process.

### The Latent Space Made Explicit

**What's hidden in current approaches:**

Inside the LLM when you say "build authentication," its internal representation might include:
- Concepts: authentication, authorization, sessions, tokens, security
- Patterns: repository, service layer, middleware
- Tradeoffs: security vs usability, performance vs correctness
- Defaults: JWT because it's common, bcrypt because it's standard

**None of this is visible to you.** The LLM makes all these choices based on its training distribution.

**With intermediate representations:**

You explicitly state:
```alloy
// YOUR domain model - your rules
sig User { credentials: Credentials }
sig Session { user: User, expiresAt: Time }

pred validAuthentication[s: Session, c: Credentials] {
    // YOUR security invariants
    s.user.credentials = c
    s.expiresAt > now
}
```

```
// YOUR architecture - your decisions
service AuthenticationService {
    pattern: stateless
    session_storage: jwt_token
    credentials: bcrypt_hashed
    
    flow:
        1. validate_credentials
        2. generate_session_token
        3. set_expiration
}
```

**Now the LLM is constrained.** It can't choose OAuth2 when you said stateless JWT. It can't use sessions when you specified tokens. It can't use MD5 when you specified bcrypt.

**The latent space reasoning that was hidden is now constrained by your explicit reasoning.**

The LLM isn't making architectural decisions - it's **implementing the decisions you already made**, filling in mechanical details (variable names, error messages, logging) that follow from your specifications.

### Why This Preserves "Soul"

Going back to the intent question: **The work has "soul" when human intent shapes meaningful decisions.**

**In the "AI handles everything" model:**
- AI chooses architecture → No soul
- AI designs domain model → No soul
- AI decides error handling → No soul
- AI makes every decision except "build authentication" → No soul

**In the intermediate representation model:**
- You formalize domain rules (Layer 2) → Your intent captured
- You design architecture (Layer 3) → Your intent captured
- You specify control flow (Layer 3) → Your intent captured
- AI fills mechanical details (Layer 4-5) → Execution of YOUR intent

**The code has soul because you made the decisions that define what the system IS.**

The specific variable names and SQL syntax don't matter - those aren't where the system's essence lives. The essence is in the invariants, the architecture, the control flow - the parts you specified explicitly.

## Current State: Natural Language Specifications

### The Problem with Unstructured Prompts

**Current approach:**
```
"Create a user repository with CRUD operations using PostgreSQL"
```

**What's ambiguous:**
- Error handling strategy (return errors? exceptions? panic?)
- Transaction boundaries (per-operation? manual control?)
- Connection management (pooling? single connection?)
- Validation timing (before persistence? at creation?)
- Null handling (nullable fields? required fields?)
- ID generation (database? UUID? provided by caller?)

**AI makes arbitrary choices** for all of these, and you can't verify them without reading generated code line-by-line.

### Semi-Structured Approaches (Emerging)

**DSPy-style signatures:**
```python
class UserRepository(dspy.Signature):
    """Repository for user data with CRUD operations"""
    
    user: dspy.InputField(desc="User entity with id, email, name")
    operation: dspy.InputField(desc="create, read, update, or delete")
    result: dspy.OutputField(desc="operation result or error")
```

**Better, but still vague:**
- What does "User entity" mean structurally?
- What error types exist?
- What are transaction semantics?
- How do failures propagate?

**The improvement:**
Input/output types are explicit, operations are enumerated, but implementation semantics are still described in English prose that AI interprets.

## Near-Future: Formalized Pseudocode with Structural Contracts

### Design Philosophy

**Goal:** Write specifications at abstraction level where you can **verify structure without reading implementation**.

**Key insight from Go:** Structural typing (duck typing) means you can specify **shapes** without specifying concrete types. Implementation can add context-specific details while satisfying core shape.

### Level 1: Type Contracts with Structural Constraints

**Specification language:**
```
type User {
    id: string
        constraints: [non_empty, unique]
    
    email: string
        constraints: [non_empty, valid_format]
        format: email_rfc5322
    
    created_at: timestamp
        constraints: [immutable, auto_assigned]
}
```

**Compiles to Go interface:**
```go
// Generated interface that implementations must satisfy
type User interface {
    GetID() string       // constraint: non-empty, unique
    GetEmail() string    // constraint: email format
    GetCreatedAt() time.Time  // constraint: immutable
}

// Generated validation
type UserValidator interface {
    ValidateUser(u User) error
}
```

**LLM generates concrete implementation:**
```go
type user struct {
    id        string
    email     string
    createdAt time.Time
    
    // LLM can add context-appropriate fields
    passwordHash string
    lastLogin    *time.Time
    roles        []string
}

// Must implement User interface (duck typing)
func (u *user) GetID() string { return u.id }
func (u *user) GetEmail() string { return u.email }
func (u *user) GetCreatedAt() time.Time { return u.createdAt }

// Generated validation satisfies constraints
func (v *userValidator) ValidateUser(u User) error {
    if u.GetID() == "" {
        return errors.New("id cannot be empty")
    }
    if !isValidEmail(u.GetEmail()) {
        return errors.New("invalid email format")
    }
    // Uniqueness check would query storage
    return nil
}
```

**Structural verification:**

You can verify generated code satisfies spec **without reading implementation**:

```bash
$ verify-spec user.spec user.go

✓ Type user implements User interface
✓ GetID() validates non-empty constraint
✓ GetEmail() validates email format
✓ GetCreatedAt() returns immutable value
✓ All constraints enforced in validator

Generated implementation: VALID
```

**Why duck typing matters here:**

The concrete `user` struct can have additional fields (`passwordHash`, `roles`) that aren't in the spec. As long as it implements the required interface methods, it satisfies the contract.

**Intent preservation:**

Your intent: "Users have IDs and emails with these constraints"
Not your intent: "Users have exactly these fields and no others"

Duck typing allows generated code to add context-appropriate details while respecting your core intent.

### Level 2: Behavioral Contracts with Pre/Post Conditions

**Specification language:**
```
interface UserRepository {
    create(user: User) -> Result<User, Error>
        requires:
            user.id == "" OR user.id not_exists_in_storage
            user.email.valid
        ensures:
            result.ok -> result.value.id != ""
            result.ok -> result.value in storage
            result.error -> storage unchanged
        
    find_by_id(id: string) -> Result<User, Error>
        requires:
            id != ""
        ensures:
            result.ok -> result.value.id == id
            result.error -> (id not_in_storage OR storage_error)
}
```

**Compiles to Go interface with contract documentation:**
```go
type UserRepository interface {
    // Create persists a new user.
    // Requires: user.GetID() == "" OR user does not exist
    //           user passes validation
    // Ensures: Success -> returned user has assigned ID
    //          Success -> user exists in storage
    //          Failure -> storage unchanged
    Create(user User) (User, error)
    
    // FindByID retrieves user by ID.
    // Requires: id is non-empty string
    // Ensures: Success -> returned user ID matches requested ID
    //          Failure -> user doesn't exist OR storage error
    FindByID(id string) (User, error)
}
```

**LLM generates implementation:**
```go
type postgresUserRepository struct {
    db *sql.DB
}

func (r *postgresUserRepository) Create(user User) (User, error) {
    // Validate preconditions
    if user.GetID() != "" {
        exists, err := r.idExists(user.GetID())
        if err != nil {
            return nil, fmt.Errorf("checking id existence: %w", err)
        }
        if exists {
            return nil, errors.New("user with id already exists")
        }
    }
    
    if err := validateUser(user); err != nil {
        return nil, fmt.Errorf("validation failed: %w", err)
    }
    
    // Begin transaction (ensures postcondition: failure -> unchanged)
    tx, err := r.db.Begin()
    if err != nil {
        return nil, fmt.Errorf("begin transaction: %w", err)
    }
    defer tx.Rollback()
    
    // Generate ID if needed (ensures postcondition: result.id != "")
    id := user.GetID()
    if id == "" {
        id = generateUUID()
    }
    
    // Insert
    _, err = tx.Exec(
        "INSERT INTO users (id, email, created_at) VALUES ($1, $2, $3)",
        id, user.GetEmail(), user.GetCreatedAt(),
    )
    if err != nil {
        return nil, fmt.Errorf("insert user: %w", err)
    }
    
    if err := tx.Commit(); err != nil {
        return nil, fmt.Errorf("commit transaction: %w", err)
    }
    
    // Return user with assigned ID (satisfies postcondition)
    return &persistedUser{
        id:        id,
        email:     user.GetEmail(),
        createdAt: user.GetCreatedAt(),
    }, nil
}

func (r *postgresUserRepository) FindByID(id string) (User, error) {
    // Validate precondition
    if id == "" {
        return nil, errors.New("id cannot be empty")
    }
    
    var u persistedUser
    err := r.db.QueryRow(
        "SELECT id, email, created_at FROM users WHERE id = $1",
        id,
    ).Scan(&u.id, &u.email, &u.createdAt)
    
    if err == sql.ErrNoRows {
        return nil, fmt.Errorf("user not found: %s", id)
    }
    if err != nil {
        return nil, fmt.Errorf("query user: %w", err)
    }
    
    // Postcondition satisfied: returned user ID matches
    return &u, nil
}
```

**Structural verification via testing:**

Generated test suite from contracts:

```go
func TestUserRepository_Create_Contracts(t *testing.T) {
    repo := setupTestRepo(t)
    
    t.Run("precondition: valid user creates successfully", func(t *testing.T) {
        user := &testUser{email: "test@example.com"}
        result, err := repo.Create(user)
        
        require.NoError(t, err)
        assert.NotEmpty(t, result.GetID()) // postcondition
        
        // Verify in storage
        found, _ := repo.FindByID(result.GetID())
        assert.Equal(t, result.GetID(), found.GetID())
    })
    
    t.Run("precondition violation: invalid email fails", func(t *testing.T) {
        user := &testUser{email: "not-an-email"}
        _, err := repo.Create(user)
        
        assert.Error(t, err) // precondition violation
    })
    
    t.Run("postcondition: failure leaves storage unchanged", func(t *testing.T) {
        // Setup: existing user
        existing := &testUser{id: "123", email: "exists@example.com"}
        repo.Create(existing)
        
        // Attempt duplicate
        duplicate := &testUser{id: "123", email: "other@example.com"}
        _, err := repo.Create(duplicate)
        
        require.Error(t, err)
        
        // Verify storage unchanged
        found, _ := repo.FindByID("123")
        assert.Equal(t, "exists@example.com", found.GetEmail())
    })
}

func TestUserRepository_FindByID_Contracts(t *testing.T) {
    repo := setupTestRepo(t)
    
    t.Run("precondition: empty id fails", func(t *testing.T) {
        _, err := repo.FindByID("")
        assert.Error(t, err)
    })
    
    t.Run("postcondition: found user ID matches", func(t *testing.T) {
        user := &testUser{email: "test@example.com"}
        created, _ := repo.Create(user)
        
        found, err := repo.FindByID(created.GetID())
        require.NoError(t, err)
        assert.Equal(t, created.GetID(), found.GetID())
    })
}
```

**You verify structure, not implementation:**

- Does `Create` check preconditions? ✓
- Does it assign IDs when needed? ✓
- Does it use transactions (storage unchanged on failure)? ✓
- Does `FindByID` validate input? ✓
- Does returned user ID match request? ✓

You don't care about:
- Specific SQL syntax
- Error message wording
- Variable names
- Whether it uses prepared statements

**Intent preserved:**

Your intent: "Repository enforces these business rules and maintains these invariants"
Not your intent: "Repository uses exactly this SQL dialect with these query patterns"

### Level 3: Architectural Patterns with Design Constraints

**Specification language:**
```
component UserService {
    architecture: layered
    
    dependencies: {
        repository: UserRepository
        validator: UserValidator
        emailer: EmailService
    }
    
    injection: constructor
    
    operations: {
        register_user(email: string, password: string) -> Result<User, Error>
            pattern: transaction_script
            flow:
                1. validate_email_format(email)
                2. check_email_not_exists(repository)
                3. hash_password(password)
                4. create_user(repository)
                5. send_welcome_email(emailer)
            
            error_handling:
                validation_failure -> return immediately
                repository_failure -> rollback
                email_failure -> log but succeed
        
        authenticate(email: string, password: string) -> Result<Session, Error>
            pattern: transaction_script
            flow:
                1. find_user_by_email(repository)
                2. verify_password_hash(password)
                3. create_session()
            
            error_handling:
                user_not_found -> return auth_error
                invalid_password -> return auth_error
    }
}
```

**Compiles to Go structure:**
```go
// Generated interface
type UserService interface {
    RegisterUser(email, password string) (User, error)
    Authenticate(email, password string) (Session, error)
}

// Generated concrete type
type userService struct {
    repository UserRepository
    validator  UserValidator
    emailer    EmailService
}

// Constructor enforces dependency injection
func NewUserService(
    repo UserRepository,
    validator UserValidator,
    emailer EmailService,
) UserService {
    return &userService{
        repository: repo,
        validator:  validator,
        emailer:    emailer,
    }
}
```

**LLM generates implementation following specified flow:**
```go
func (s *userService) RegisterUser(email, password string) (User, error) {
    // Step 1: validate email format
    if err := s.validator.ValidateEmail(email); err != nil {
        return nil, fmt.Errorf("invalid email: %w", err)
    }
    
    // Step 2: check email not exists
    existing, err := s.repository.FindByEmail(email)
    if err != nil && !errors.Is(err, ErrNotFound) {
        // Repository failure -> cannot proceed
        return nil, fmt.Errorf("check email existence: %w", err)
    }
    if existing != nil {
        return nil, errors.New("email already registered")
    }
    
    // Step 3: hash password
    hash, err := hashPassword(password)
    if err != nil {
        return nil, fmt.Errorf("hash password: %w", err)
    }
    
    // Step 4: create user
    user := &user{
        email:        email,
        passwordHash: hash,
        createdAt:    time.Now(),
    }
    
    created, err := s.repository.Create(user)
    if err != nil {
        return nil, fmt.Errorf("create user: %w", err)
    }
    
    // Step 5: send welcome email (failure logged but not returned)
    if err := s.emailer.SendWelcome(email); err != nil {
        log.Printf("failed to send welcome email to %s: %v", email, err)
        // Continue - email failure doesn't fail registration
    }
    
    return created, nil
}

func (s *userService) Authenticate(email, password string) (Session, error) {
    // Step 1: find user by email
    user, err := s.repository.FindByEmail(email)
    if err != nil {
        if errors.Is(err, ErrNotFound) {
            // User not found -> auth error (don't reveal which)
            return nil, ErrAuthenticationFailed
        }
        return nil, fmt.Errorf("find user: %w", err)
    }
    
    // Step 2: verify password
    if !verifyPasswordHash(user.GetPasswordHash(), password) {
        return nil, ErrAuthenticationFailed
    }
    
    // Step 3: create session
    session := &session{
        userID:    user.GetID(),
        createdAt: time.Now(),
        expiresAt: time.Now().Add(24 * time.Hour),
    }
    
    return session, nil
}
```

**Structural verification:**

```bash
$ verify-spec user_service.spec user_service.go

✓ UserService has dependencies: UserRepository, UserValidator, EmailService
✓ Dependencies injected via constructor
✓ RegisterUser follows 5-step flow
  ✓ Step 1: validates email format
  ✓ Step 2: checks email not exists
  ✓ Step 3: hashes password
  ✓ Step 4: creates user in repository
  ✓ Step 5: sends welcome email
✓ Error handling: validation failures return immediately
✓ Error handling: repository failures cause rollback
✓ Error handling: email failures logged but don't fail operation
✓ Authenticate follows 3-step flow
  ✓ Step 1: finds user by email
  ✓ Step 2: verifies password hash
  ✓ Step 3: creates session
✓ Error handling: not found returns auth error
✓ Error handling: invalid password returns auth error

Generated implementation: VALID
```

**Intent preserved:**

Your intent: "Service coordinates these dependencies in this order with this error handling"
Not your intent: "Service uses these specific function names and error messages"

The **structure of the control flow** matches your specification. The mechanical details (logging format, variable names, exact error types) are generated appropriately.

### Python Example: OO Patterns with Duck Typing

**Specification (same language):**
```
class User {
    attributes: {
        id: string [readonly, unique]
        email: string [required, validated(email_format)]
        created_at: datetime [readonly, auto_assigned]
    }
    
    methods: {
        validate() -> bool
            ensures: returns true IFF all constraints satisfied
    }
}

class UserRepository {
    pattern: repository
    
    methods: {
        create(user: User) -> User
            requires: user.validate()
            ensures: result.id is assigned
        
        find_by_id(id: string) -> Optional<User>
            requires: id != ""
            ensures: result.id == id OR result is None
    }
}
```

**Compiles to Python with duck typing:**
```python
# Generated abstract base (optional - Python uses duck typing)
class User(Protocol):
    @property
    def id(self) -> str: ...
    
    @property
    def email(self) -> str: ...
    
    @property
    def created_at(self) -> datetime: ...
    
    def validate(self) -> bool: ...

# Generated concrete implementation
class UserImpl:
    def __init__(self, email: str, id: Optional[str] = None):
        self._id = id or ""
        self._email = email
        self._created_at = datetime.now()
        
        # LLM can add context-appropriate attributes
        self._is_active = True
        self._roles: List[str] = []
    
    @property
    def id(self) -> str:
        return self._id
    
    @property
    def email(self) -> str:
        return self._email
    
    @property
    def created_at(self) -> datetime:
        return self._created_at
    
    def validate(self) -> bool:
        """Ensures: returns true IFF all constraints satisfied"""
        if not self._email:
            return False
        if not self._is_valid_email(self._email):
            return False
        return True
    
    @staticmethod
    def _is_valid_email(email: str) -> bool:
        # Generated validation logic
        import re
        pattern = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'
        return re.match(pattern, email) is not None
```

**Repository implementation:**
```python
class UserRepository(Protocol):
    def create(self, user: User) -> User: ...
    def find_by_id(self, id: str) -> Optional[User]: ...

class PostgresUserRepository:
    def __init__(self, connection_string: str):
        self.conn = psycopg2.connect(connection_string)
    
    def create(self, user: User) -> User:
        """
        Requires: user.validate()
        Ensures: result.id is assigned
        """
        # Validate precondition
        if not user.validate():
            raise ValueError("User validation failed")
        
        # Generate ID if needed
        user_id = user.id or str(uuid.uuid4())
        
        with self.conn.cursor() as cur:
            cur.execute(
                "INSERT INTO users (id, email, created_at) VALUES (%s, %s, %s)",
                (user_id, user.email, user.created_at)
            )
            self.conn.commit()
        
        # Return user with assigned ID (postcondition satisfied)
        return UserImpl(email=user.email, id=user_id)
    
    def find_by_id(self, id: str) -> Optional[User]:
        """
        Requires: id != ""
        Ensures: result.id == id OR result is None
        """
        if not id:
            raise ValueError("ID cannot be empty")
        
        with self.conn.cursor() as cur:
            cur.execute(
                "SELECT id, email, created_at FROM users WHERE id = %s",
                (id,)
            )
            row = cur.fetchone()
        
        if row is None:
            return None
        
        # Postcondition: result.id == id
        return UserImpl(email=row[1], id=row[0])
```

**Duck typing advantage:**

`PostgresUserRepository` doesn't explicitly inherit from `UserRepository` protocol, but it satisfies the interface through duck typing. Python's type checker verifies structural compatibility:

```python
def process_user(repo: UserRepository, user_id: str):
    user = repo.find_by_id(user_id)  # Type checker validates
    if user:
        print(f"Found: {user.email}")

# Works with any object that has the right methods
postgres_repo = PostgresUserRepository("postgresql://...")
process_user(postgres_repo, "123")  # ✓ Type checks
```

**Verification still works:**

```python
# Generated test suite
class TestUserRepository:
    def test_create_precondition_validation(self):
        repo = PostgresUserRepository(TEST_DB)
        invalid_user = UserImpl(email="")  # Invalid
        
        with pytest.raises(ValueError):
            repo.create(invalid_user)
    
    def test_create_postcondition_id_assigned(self):
        repo = PostgresUserRepository(TEST_DB)
        user = UserImpl(email="test@example.com", id="")
        
        result = repo.create(user)
        assert result.id != ""  # Postcondition
    
    def test_find_by_id_precondition_empty_id(self):
        repo = PostgresUserRepository(TEST_DB)
        
        with pytest.raises(ValueError):
            repo.find_by_id("")
    
    def test_find_by_id_postcondition_id_matches(self):
        repo = PostgresUserRepository(TEST_DB)
        user = UserImpl(email="test@example.com")
        created = repo.create(user)
        
        found = repo.find_by_id(created.id)
        assert found is not None
        assert found.id == created.id  # Postcondition
```

## Integration with Formal Methods

### Two-Layer Specification Strategy

**Problem:** The pseudocode specs above are still informal. "Valid email" is English prose, not formal logic.

**Solution:** Layer formal domain models underneath structural specifications.

### Layer 1: Formal Domain Model (Alloy)

```alloy
// domain.als - Formal properties
sig User {
    id: String,
    email: String,
    createdAt: Time
}

pred validEmail[e: String] {
    // Formal definition of valid email
    some e
    e in EmailFormat
}

pred validUser[u: User] {
    some u.id
    validEmail[u.email]
    u.createdAt in PastOrPresent
}

// Repository invariants
sig UserRepository {
    users: set User
}

pred createUser[repo, repo': UserRepository, u: User] {
    // Preconditions
    validUser[u]
    u not in repo.users
    
    // Postcondition
    repo'.users = repo.users + u
    u.id in repo'.users.id
}

assert createPreservesValidity {
    all repo, repo': UserRepository, u: User |
        createUser[repo, repo', u] implies
        all u': repo'.users | validUser[u']
}

check createPreservesValidity for 5
```

**Alloy model checker verifies:**
- All reachable states satisfy invariants
- Preconditions are necessary
- Postconditions are sufficient
- No edge cases violate properties

**Generates traces:**
```
Checking createPreservesValidity...
  Instance found (satisfying example):
    User: {User$0, User$1}
    id: {User$0->id$0, User$1->id$1}
    email: {User$0->email$0, User$1->email$1}
    ...
  
  Counterexample (property violation):
    [None found - property holds]
```

### Layer 2: Structural Specification (Pseudocode)

```
// References formal model
type User from domain.als.User {
    // Formal constraints from Alloy
    constraints: domain.als.validUser
    
    // Additional structural requirements
    serialization: json
    persistence: database_backed
}

interface UserRepository from domain.als.UserRepository {
    create(user: User) -> Result<User, Error>
        // Formal preconditions from Alloy
        requires: domain.als.createUser.preconditions
        
        // Formal postconditions from Alloy
        ensures: domain.als.createUser.postconditions
        
        // Implementation guidance
        error_handling: explicit
        transactions: required
}
```

### Combined Verification

**Step 1: Alloy verification**
```bash
$ alloy check domain.als
✓ All assertions hold
✓ No property violations found
Generated 23 test traces
```

**Step 2: Generate code from specs**
```bash
$ compile-spec --alloy domain.als --struct repo.spec --target go
Generated: user.go
Generated: user_repository.go
Generated: user_test.go (from Alloy traces)
```

**Step 3: Verify structural properties**
```bash
$ verify-spec repo.spec user_repository.go
✓ Type UserImpl satisfies domain.als.User invariants
✓ create() enforces domain.als.createUser preconditions
✓ create() satisfies domain.als.createUser postconditions
✓ Generated tests cover Alloy traces
```

**Step 4: Run tests**
```bash
$ go test
PASS: TestCreate_AlloyTrace_1
PASS: TestCreate_AlloyTrace_2
...
PASS: TestCreate_AlloyTrace_23
PASS: TestCreate_PreconditionViolation
PASS: TestCreate_PostconditionSatisfied
```

**The guarantee:**

If Alloy verification passes AND structural verification passes AND tests pass:
- Domain properties provably hold
- Implementation satisfies contracts
- Generated code is correct with respect to spec

**Not "code might be right" - but "code is provably right within model".**

## Practical Workflow Example

### Complete Example: Building a Payment System

**Step 1: Define domain model formally**

```alloy
// payment_domain.als
sig Money {
    amount: Int,
    currency: Currency
}

sig Currency {}

sig Account {
    id: String,
    balance: Money
}

pred validAccount[a: Account] {
    some a.id
    a.balance.amount >= 0
}

pred transfer[
    from, from': Account,
    to, to': Account,
    amount: Money
] {
    // Preconditions
    validAccount[from]
    validAccount[to]
    from.balance.amount >= amount.amount
    from.balance.currency = amount.currency
    
    // Postconditions
    from'.balance.amount = from.balance.amount - amount.amount
    to'.balance.amount = to.balance.amount + amount.amount
    from'.id = from.id
    to'.id = to.id
}

assert transferPreservesTotalBalance {
    all from, from', to, to': Account, amount: Money |
        transfer[from, from', to, to', amount] implies
        (from.balance.amount + to.balance.amount) =
        (from'.balance.amount + to'.balance.amount)
}

check transferPreservesTotalBalance for 5
```

**Step 2: Define structural specifications**

```
// payment.spec

type Money from payment_domain.als.Money {
    fields: {
        amount: decimal(precision=2)
        currency: string(length=3)
    }
    
    constraints: payment_domain.als.validMoney
    
    serialization: json
    validation: on_construction
}

type Account from payment_domain.als.Account {
    fields: {
        id: uuid
        balance: Money
    }
    
    constraints: payment_domain.als.validAccount
    
    persistence: database_backed
    concurrency: optimistic_locking
}

service PaymentService {
    dependencies: {
        accounts: AccountRepository
        audit: AuditLog
    }
    
    operations: {
        transfer(
            from_id: uuid,
            to_id: uuid,
            amount: Money
        ) -> Result<Transaction, Error>
            
            // References formal preconditions
            requires: payment_domain.als.transfer.preconditions
            
            // Additional structural requirements
            requires: from_id != to_id
            
            // References formal postconditions
            ensures: payment_domain.als.transfer.postconditions
            
            // Implementation guidance
            pattern: transaction_script
            isolation: serializable
            
            flow:
                1. load_accounts(from_id, to_id) with_lock
                2. validate_sufficient_balance(from_account, amount)
                3. deduct_from_source(from_account, amount)
                4. add_to_destination(to_account, amount)
                5. record_transaction(audit)
                6. commit_changes()
            
            error_handling:
                insufficient_balance -> rollback, return error
                account_not_found -> rollback, return error
                concurrent_modification -> retry(max_attempts=3)
    }
}
```

**Step 3: Verify formal model**

```bash
$ alloy check payment_domain.als

Checking transferPreservesTotalBalance for 5...
   No counterexample found.
   
Checking transferRequiresSufficientBalance for 5...
   No counterexample found.

✓ All assertions verified
Generated 15 test traces
```

**Step 4: Compile to Go**

```bash
$ compile-spec \
    --alloy payment_domain.als \
    --struct payment.spec \
    --target go \
    --output ./generated

Generating from specifications...
✓ Parsed Alloy model
✓ Extracted formal properties  
✓ Parsed structural specifications
✓ Validated spec consistency

Generating Go code...
✓ Generated types: Money, Account
✓ Generated interfaces: AccountRepository, AuditLog
✓ Generated service: PaymentService
✓ Generated validators from Alloy constraints
✓ Generated tests from Alloy traces (15 test cases)

Output written to ./generated/
```

**Step 5: Review generated structure** (not line-by-line)

```bash
$ tree generated/
generated/
├── money.go              # Money type with validation
├── account.go            # Account type with constraints
├── account_repository.go # Repository interface
├── payment_service.go    # Service implementation
└── payment_test.go       # Generated tests

$ verify-spec payment.spec generated/payment_service.go

Verifying structural compliance...

✓ PaymentService has required dependencies
  ✓ AccountRepository injected
  ✓ AuditLog injected

✓ Transfer method flow validated
  ✓ Step 1: Loads accounts with locking
  ✓ Step 2: Validates balance
  ✓ Step 3: Deducts from source
  ✓ Step 4: Adds to destination
  ✓ Step 5: Records in audit log
  ✓ Step 6: Commits transaction

✓ Error handling verified
  ✓ Insufficient balance causes rollback
  ✓ Not found causes rollback
  ✓ Concurrent modification triggers retry (max 3)

✓ Formal properties enforced
  ✓ Preconditions checked in code
  ✓ Postconditions maintained
  ✓ Invariants preserved

Generated code: STRUCTURALLY VALID
```

**Step 6: Run verification tests**

```bash
$ cd generated && go test -v

=== RUN TestTransfer_AlloyTrace_1
--- PASS: TestTransfer_AlloyTrace_1 (0.01s)

=== RUN TestTransfer_AlloyTrace_2
--- PASS: TestTransfer_AlloyTrace_2 (0.01s)

... [13 more Alloy trace tests] ...

=== RUN TestTransfer_PreconditionViolation_InsufficientBalance
--- PASS: TestTransfer_PreconditionViolation_InsufficientBalance (0.00s)

=== RUN TestTransfer_PostconditionSatisfied_BalancePreserved
--- PASS: TestTransfer_PostconditionSatisfied_BalancePreserved (0.01s)

=== RUN TestTransfer_ConcurrentModification_Retries
--- PASS: TestTransfer_ConcurrentModification_Retries (0.03s)

PASS
ok      payment 0.234s
```

**What you verified without reading implementation:**

✓ Domain properties hold (Alloy proved it)
✓ Code structure matches specification (structural verifier checked)
✓ Error handling follows specified patterns (structural verifier checked)
✓ Control flow follows specified steps (structural verifier checked)
✓ Generated tests pass (Go test runner confirmed)

**What you DON'T need to verify:**

✗ Variable naming conventions
✗ Specific SQL syntax
✗ Error message wording
✗ Logging format
✗ Code comments

**Intent preserved:**

Your intent:
- "Transfer money between accounts"
- "Preserve total balance (formal invariant)"
- "Handle concurrency with optimistic locking"
- "Follow this error handling strategy"
- "Execute these steps in this order"

Not your intent:
- "Use these specific variable names"
- "Write SQL queries this exact way"
- "Format error messages like this"

**The generated implementation reflects your architectural and domain intent** while handling mechanical details appropriately.

## The Two Futures

### Future 1: "AI Handles Everything" (The Black Box Path)

**What it promises:**
- No need to learn formal methods, architectural patterns, or programming
- Just describe what you want, AI handles the rest
- Democratizes software development
- Fast time to working code

**What it delivers:**

**Scenario 1: Complete Dependency**

Systems become unmaintainable by humans. When the AI that generated it is gone (company shut down, API deprecated, model obsolete), the code becomes archaeological artifacts no one understands.

**Scenario 2: Tribal Knowledge in Prompts**

The only "specification" is ChatGPT conversation history. Companies hoard prompt libraries like medieval guilds hoarded trade secrets. Knowledge transfer becomes "here's the magic prompt that generates our auth system."

**Scenario 3: Architectural Drift**

Each generation slightly misinterprets the last. Like a game of telephone, the system slowly drifts from original intent. No one notices until catastrophic failure because there's no specification to compare against.

**Scenario 4: Verification Impossibility**

You can only test, never verify. Every bug is a surprise. Security vulnerabilities are found by attackers, not prevented by design. Regulatory compliance becomes "we think the AI did it right but can't prove it."

**Scenario 5: Innovation Stagnation**

If you can't understand or modify the abstractions the system uses, you can't improve them. Progress becomes "use newer AI model" rather than "better understanding of problem domain."

**Scenario 6: Loss of Agency**

Developers become prompt engineers, hoping AI guesses correctly. Architectural decisions are made by AI defaults based on training distribution, not human judgment about what's appropriate for this specific system.

**The underlying problem:**

This path treats the LLM's internal reasoning as fundamentally opaque and accepts it. You put intent in natural language on one end, hope for correct code on the other, and have no visibility into or control over the reasoning that connects them.

### Future 2: "Intermediate Representations Preserve Human Agency"

**What it requires:**
- Learning to formalize domain rules (Alloy, TLA+)
- Thinking architecturally (patterns, flows, constraints)
- Understanding verification (testing vs proving)
- More upfront design work

**What it delivers:**

**Scenario 1: Understandable Systems**

Even if original developers leave, formal models and structural specifications document system intent. New developers can understand WHY things work the way they do, not just THAT they work.

**Scenario 2: Composable Knowledge**

Pattern libraries and domain models become shared resources. "Implement repository pattern" works consistently because the pattern is formalized. Knowledge compounds rather than fragmenting into prompt libraries.

**Scenario 3: Provable Correctness**

Security-critical systems can be formally verified. Healthcare systems prove they maintain HIPAA requirements. Financial systems prove they don't lose money in transfers. Regulatory compliance becomes "here's the formal proof."

**Scenario 4: Evolutionary Design**

When requirements change, modify specifications and regenerate. System stays coherent because specifications define coherence. Technical debt is "specs that don't match reality" (detectable) not "code no one understands" (invisible until it breaks).

**Scenario 5: Innovation Through Understanding**

Better domain models → better systems. Better architectural patterns → better code. New abstractions can be formalized and shared. Progress comes from human understanding deepening, with AI accelerating implementation.

**Scenario 6: Preserved Agency**

Humans are system designers making explicit choices at appropriate abstraction levels. AI is implementation accelerator working within constraints. Code reflects human architectural decisions, not AI defaults.

**The underlying principle:**

This path makes the LLM's reasoning explicit and human-controllable through layered specifications at multiple abstraction levels. Each layer captures different kinds of intent in verifiable form.

## Why This Matters: The Stakes

### The Verification Scaling Problem

**Current approaches:**
- Read every line of generated code (doesn't scale)
- Trust and hope (creates technical debt and security holes)
- Iterate via prompting (loses design coherence)

**This approach:**
- Verify formal properties (Alloy proves it)
- Verify structural properties (AST analysis confirms it)
- Verify behavioral properties (generated tests check it)
- Never read line-by-line unless debugging

### The Skill Development Problem

**Current AI coding:**
- Novices get code they don't understand (false mastery)
- Experts get frustrated by AI's arbitrary choices
- No middle ground

**This approach:**
- Forces thinking at architectural level (builds real skill)
- Builds mental models through specification (actual understanding)
- AI accelerates but doesn't replace understanding
- Can always drop down to implementation when needed

### The Maintainability Problem

**Current generated code:**
- Hard to modify (need to re-prompt, hope AI interprets correctly)
- Hard to extend (don't understand structure deeply enough)
- Hard to debug (implementation details opaque)

**This approach:**
- Modify specification, regenerate (deterministic)
- Specification IS documentation (always up to date)
- Structure is explicit and verified (AST confirms it)
- Can inspect/modify generated code (not locked in)

### The Intent Preservation Problem

**Current AI coding:**
- Generates complete implementations from vague descriptions
- Human in review mode, not design mode
- Architectural decisions made by AI defaults
- Code reflects AI's interpretation, not human's intent
- No way to verify intent was preserved

**This approach:**
- Human specifies at architectural abstraction level
- AI generates mechanical details within constraints
- Human verifies structure, not syntax
- Code reflects human's design decisions
- Intent is captured in verifiable specifications

## Tooling Architecture

### Complete Toolchain

```
┌─────────────────────────────────────────────┐
│  Specification Files                        │
│  - domain.als (Alloy model)                 │
│  - system.spec (Structural specs)           │
└──────────────┬──────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────┐
│  Verification Layer                         │
│  - Alloy Analyzer (formal verification)     │
│  - Spec Parser (parse structural specs)     │
│  - Consistency Checker (Alloy ↔ specs)      │
└──────────────┬──────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────┐
│  Code Generation Layer                      │
│  - LLM Generator (implementation synthesis) │
│  - Template Engine (boilerplate)            │
│  - Test Generator (from Alloy traces)       │
└──────────────┬──────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────┐
│  Generated Artifacts                        │
│  - Source code (Go/Python/etc)              │
│  - Test suites                              │
│  - Documentation                            │
└──────────────┬──────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────┐
│  Structural Verification Layer              │
│  - AST Analysis (verify structure)          │
│  - Contract Checker (pre/post conditions)   │
│  - Flow Validator (control flow matches)    │
└──────────────┬──────────────────────────────┘
               │
               ↓
┌─────────────────────────────────────────────┐
│  Testing Layer                              │
│  - Unit tests (generated + manual)          │
│  - Integration tests                        │
│  - Property-based tests (from Alloy)        │
└─────────────────────────────────────────────┘
```

### Editor Integration

**VSCode Extension:**
```
payment.spec
├── Syntax highlighting for spec language
├── Live errors from Alloy analyzer
├── "Generate Code" command
├── Inline verification results
└── Jump to generated implementation

payment_service.go (generated)
├── Link to specification
├── Verification status badge
├── "Regenerate" command
└── "Show spec" command
```

**View Modes:**

**Mode 1: Specification View**
```
// payment.spec [VERIFIED ✓]

service PaymentService {
    operations: {
        transfer(...) -> Result<Transaction, Error>
            requires: ...
            ensures: ...
            flow: [6 steps]
    }
}

[Show Generated Implementation ▼]  [Regenerate]
```

**Mode 2: Implementation View**
```go
// payment_service.go [GENERATED FROM: payment.spec]

type PaymentService struct { ... }

func (s *PaymentService) Transfer(...) (Transaction, error) {
    // Generated implementation
    // ...
}

[Show Specification ▲]  [Verify Structure]  [Run Tests]
```

**Mode 3: Side-by-Side**
```
┌─────────────────────┬──────────────────────┐
│ payment.spec        │ payment_service.go   │
│                     │                      │
│ transfer(...)       │ func Transfer(...)   │
│   requires:         │   if !validate(...) {│
│     balance > amt   │     return err       │
│   ensures:          │   }                  │
│     balance' = ...  │   newBal := ...      │
│                     │   return ...         │
└─────────────────────┴──────────────────────┘
       [Verify Mapping: ✓]
```

## Current Implementation Feasibility

### What Exists Today

**Alloy/Forge:**
- Mature formal verification
- Active development
- Good documentation
- Educational resources

**LLM Code Generation:**
- GPT-4, Claude, etc. can generate from descriptions
- Quality varies but improving rapidly
- Best with clear constraints

**AST Analysis:**
- Go's `go/ast` package (excellent)
- Python's `ast` module (excellent)
- Can verify structural properties programmatically

**Testing Frameworks:**
- Property-based testing (Hypothesis, QuickCheck)
- Can generate tests from specifications

### What Needs Building

**Specification Language Parser:**
- Parse pseudocode specs
- Extract contracts, constraints, flows
- Link to Alloy models
- **Difficulty:** Medium (standard parsing problem)

**LLM Prompt Construction:**
- Convert specs to effective prompts
- Include Alloy properties as constraints
- Generate multiple candidates
- **Difficulty:** Medium (prompt engineering + orchestration)

**Structural Verifier:**
- Parse generated AST
- Check against specification
- Verify control flow matches
- Verify contracts enforced
- **Difficulty:** Medium-High (requires domain knowledge)

**Test Generator:**
- Convert Alloy traces to unit tests
- Generate property-based tests
- Create integration test scaffolding
- **Difficulty:** Medium (code generation)

**Editor Tooling:**
- VSCode extension
- Syntax highlighting
- Live verification feedback
- **Difficulty:** Low-Medium (standard editor extension)

### Estimated Timeline

**Phase 1 (2-3 months): Proof of Concept**
- Minimal spec language parser
- Basic Alloy integration
- Simple LLM generation pipeline
- Structural verification for Go
- Hand-written test suite

**Phase 2 (3-4 months): Core Features**
- Complete spec language
- Multi-target generation (Go, Python)
- Automated test generation
- Basic editor support

**Phase 3 (4-6 months): Polish & Ecosystem**
- Pattern libraries
- Domain-specific extensions
- Advanced editor features
- Documentation and examples

**Total: 9-13 months to production-ready tooling**

## The Core Argument

### Why Accept the Black Box?

The "AI will write everything" narrative asks us to accept:
- Programming languages are the optimal abstraction level for human reasoning
- Human understanding of implementation details is unnecessary
- Verification through testing is sufficient
- Arbitrary AI choices based on training distribution are acceptable
- Systems we can't understand or modify are fine

**This is presented as inevitable progress. It's actually a surrender of human agency in system design.**

### The Alternative Path

Intermediate representations at multiple abstraction levels:
- Recognize that different abstraction levels serve different purposes
- Preserve human understanding at each level where design decisions matter
- Enable formal verification of properties that must hold
- Ensure generated code reflects human intent, not AI defaults
- Keep humans in the design loop at every level where intent matters

**This is not resistance to AI. It's insistence on human agency.**

## The Real Question

**Do we want a future where:**
- Humans become prompt engineers, hoping AI guesses correctly?
- Systems are black boxes we can only test, never understand?
- Knowledge is tribal lore of magic prompts?
- Maintenance means "re-prompt and hope"?
- Innovation means "wait for better AI model"?

**Or a future where:**
- Humans are system designers, making explicit choices at appropriate abstraction levels?
- Systems are understood through layered specifications we can verify?
- Knowledge is formalized in shareable, improvable artifacts?
- Maintenance means "update spec, regenerate, verify"?
- Innovation means "better understanding of abstractions"?

## Conclusion

**This work is fundamentally about:**

Making the LLM's latent space reasoning explicit and human-controllable through intermediate representations at multiple abstraction levels.

**Not because it makes AI better.**

But because **it keeps humans in the design loop at every level where intent matters.**

Each layer of specification captures different kinds of human reasoning:
- Formal domain models capture business invariants
- Structural specifications capture architectural intent
- Generated implementation satisfies both

At every step, human reasoning is:
- Explicit (written down, not implicit in prompts)
- Verifiable (formally or structurally checked)
- Preserved (serves as documentation)
- Controllable (can be modified, code regenerated)

**The code has "soul" because human intent shaped every meaningful decision.**

The AI filled in mechanical details (variable names, SQL syntax, logging) that follow from specifications, but didn't make architectural choices.

**This is the path forward:**

Not "humans write all the code" (too slow).
Not "AI writes all the code" (loss of agency and understanding).

But: **Humans design in verifiable specifications, AI implements within constraints.**

The specifications ARE the latent space made explicit. The intermediate representations ARE human reasoning made manifest.

**That's why this work matters.**

**That's why it's worth building.**
