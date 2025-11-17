# ♟️ Chess Game

A full-featured chess game built with **Next.js 15**, **TypeScript**, and **Tailwind CSS**. This project implements **SOLID principles**, **design patterns** (Repository, Adapter, Dependency Injection), and **Clean Architecture** for learning advanced software engineering concepts.

## 🎯 Project Goals

This project is designed as a learning platform to master:

- **SOLID Principles** - Writing maintainable and scalable code
- **Design Patterns** - Repository, Adapter, Strategy patterns
- **Clean Architecture** - Separation of concerns and dependency management
- **TypeScript** - Type-safe development
- **Modern React/Next.js** - Component architecture and state management

## 🚀 Tech Stack

### Current (Phase 1)
- **Framework**: Next.js 16 (App Router)
- **Language**: TypeScript 5
- **Styling**: Tailwind CSS v4
- **State Management**: React Context API
- **Storage**: Local Storage (Repository Pattern)

### Future (Phase 2 - Planned)
- **Backend**: Python FastAPI
- **Database**: PostgreSQL
- **Real-time**: WebSockets
- **Containerization**: Docker & Docker Compose
- **AI Engine**: Minimax algorithm with alpha-beta pruning

## 📁 Project Structure

```
src/
├── app/                      # Next.js App Router (Presentation Layer)
│   ├── components/
│   │   ├── chess/           # Chess-specific components
│   │   └── ui/              # Reusable UI components
│   ├── hooks/               # Custom React hooks
│   └── context/             # React Context for state management
│
├── core/                     # Application/Business Logic Layer
│   ├── usecases/            # Use cases (MakeMove, StartGame, etc)
│   └── dtos/                # Data Transfer Objects
│
├── domain/                   # Domain Layer (Business Rules)
│   ├── entities/            # Domain entities (Piece, Board, Game)
│   ├── value-objects/       # Immutable objects (Position, Move)
│   ├── services/            # Domain services (MoveValidator)
│   └── interfaces/          # Contracts for Dependency Inversion
│
├── infrastructure/           # Infrastructure Layer
│   ├── repositories/        # Data persistence implementations
│   ├── adapters/            # External format adapters (FEN, PGN)
│   └── storage/             # Storage utilities
│
└── shared/                   # Shared utilities
    ├── types/               # Common TypeScript types
    ├── constants/           # Game constants
    └── utils/               # Helper functions


## 🎨 SOLID Principles Implementation

### 1. Single Responsibility Principle (SRP)
Each class has one reason to change:
- `MoveValidator` - Only validates chess moves
- `GameEngine` - Only manages game state
- `ChessBoard` component - Only renders the board

### 2. Open/Closed Principle (OCP)
Open for extension, closed for modification:
- Abstract `Piece` class can be extended with new piece types
- New game modes can be added without modifying existing code

### 3. Liskov Substitution Principle (LSP)
Derived classes are substitutable for base classes:
- All piece classes (`King`, `Queen`, `Rook`, etc.) can substitute `Piece`
- All implementations work with `IPiece` interface

### 4. Interface Segregation Principle (ISP)
Clients shouldn't depend on interfaces they don't use:
- `IGameRepository` - Only game persistence methods
- `IMoveValidator` - Only move validation methods
- `INotationAdapter` - Only notation conversion methods

### 5. Dependency Inversion Principle (DIP)
Depend on abstractions, not concretions:
- Use cases depend on `IGameRepository` interface
- Easy to swap `LocalStorageRepository` with `ApiRepository` later

## 🎯 Design Patterns

### Repository Pattern
Abstracts data persistence logic:
```typescript
interface IGameRepository {
  save(game: Game): Promise<void>;
  load(gameId: string): Promise<Game | null>;
}

// Implementation can be swapped easily
class LocalStorageGameRepository implements IGameRepository { }
class ApiGameRepository implements IGameRepository { } // Future
```

### Adapter Pattern
Converts data between different formats:
```typescript
class FenAdapter {
  toBoardState(fen: string): Board;
  fromBoardState(board: Board): string;
}
```

### Dependency Injection
Dependencies are injected via constructors:
```typescript
class MakeMove {
  constructor(
    private gameRepository: IGameRepository,
    private moveValidator: IMoveValidator
  ) {}
}
```

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ 
- npm or yarn or pnpm

### Installation

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/chess-game.git

# Navigate to project directory
cd chess-game

# Install dependencies
npm install

# Run development server
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to see the chess game.

## 📚 Learning Resources

This project implements concepts from:
- **Clean Architecture** by Robert C. Martin
- **Design Patterns** by Gang of Four
- **Domain-Driven Design** by Eric Evans

## 🗺️ Roadmap

### Phase 1: Foundation (Current)
- [x] Project structure with Clean Architecture
- [ ] Chess board UI with drag & drop
- [ ] All chess pieces implementation
- [ ] Move validation (legal moves)
- [ ] Check and checkmate detection
- [ ] Move history and undo functionality
- [ ] Game state persistence (localStorage)

### Phase 2: AI & Advanced Features
- [ ] Minimax algorithm for AI opponent
- [ ] Difficulty levels
- [ ] Move suggestions
- [ ] FEN notation import/export
- [ ] PGN notation support
- [ ] Game analysis

### Phase 3: Multiplayer (Future)
- [ ] Python FastAPI backend
- [ ] WebSocket for real-time games
- [ ] User authentication
- [ ] Matchmaking system
- [ ] Leaderboard
- [ ] Game history
- [ ] PostgreSQL database
- [ ] Docker containerization

## 🤝 Contributing

This is a personal learning project, but suggestions and feedback are welcome! Feel free to:
- Open issues for bugs or suggestions
- Submit pull requests for improvements
- Share your learning insights

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 👨‍💻 Author

Built with ❤️ as a learning project to master software architecture principles and TypeScript development.

---

⭐ **Star this repo** if you find it helpful for learning!

## 📖 Documentation

- [Architecture Overview](docs/ARCHITECTURE.md) _(coming soon)_
- [SOLID Principles Guide](docs/SOLID.md) _(coming soon)_
- [Design Patterns Explained](docs/PATTERNS.md) _(coming soon)_
- [Chess Rules Implementation](docs/CHESS_RULES.md) _(coming soon)_
