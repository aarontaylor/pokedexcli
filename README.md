# Pokédex CLI

A command-line Pokédex application written in Go that allows you to explore the Pokémon world, catch Pokémon, and manage your collection.

## Features

- Interactive REPL (Read-Eval-Print Loop) interface
- Explore locations and discover Pokémon
- Catch Pokémon with randomized success rates
- Inspect caught Pokémon details including stats, types, and abilities
- Navigate through paginated location listings
- Efficient caching system to minimize API calls
- Thread-safe implementation

## Requirements

- Go 1.24.4 or higher
- Internet connection (for PokeAPI access)

## Installation

Clone the repository and build the application:

```bash
git clone [repository-url]
cd pokedexcli
go build -o pokedexcli
```

## Usage

Start the application:

```bash
./pokedexcli
```

You'll be greeted with an interactive prompt:

```
Pokedex > 
```

## Available Commands

| Command | Description | Example |
|---------|-------------|---------|
| `help` | Display all available commands | `help` |
| `map` | Display the next 20 locations | `map` |
| `mapb` | Display the previous 20 locations | `mapb` |
| `explore <location>` | Explore a location and see Pokémon encounters | `explore canalave-city` |
| `catch <pokemon>` | Attempt to catch a Pokémon | `catch pikachu` |
| `inspect <pokemon>` | View details of a caught Pokémon | `inspect pikachu` |
| `pokedex` | List all caught Pokémon | `pokedex` |
| `exit` | Exit the application | `exit` |

## Example Session

```
Pokedex > map
canalave-city
eterna-city
pastoria-city
...

Pokedex > explore pastoria-city
Exploring pastoria-city...
Found Pokémon:
- psyduck
- golduck
- croagunk
- toxicroak

Pokedex > catch psyduck
Throwing a Pokeball at psyduck...
psyduck was caught!
You may now inspect it with the inspect command.

Pokedex > inspect psyduck
Name: psyduck
Height: 8
Weight: 196
Stats:
  -hp: 50
  -attack: 52
  -defense: 48
  -special-attack: 65
  -special-defense: 50
  -speed: 55
Types:
  - water

Pokedex > pokedex
Your Pokedex:
  - psyduck

Pokedex > exit
Closing the Pokedex... Goodbye!
```

## Architecture

### Project Structure

```
pokedexcli/
├── main.go                 # Application entry point
├── repl.go                 # REPL implementation
├── repl_test.go           # REPL tests
├── command_*.go           # Command implementations
├── internal/
│   ├── pokeapi/          # PokeAPI client
│   │   ├── client.go     # HTTP client with caching
│   │   ├── *.go          # API methods and types
│   └── pokecache/        # Cache implementation
│       ├── pokecache.go  # Thread-safe cache
│       └── pokecache_test.go
└── go.mod                # Go module definition
```

### Key Components

- **REPL**: Provides the interactive command-line interface
- **PokeAPI Client**: Handles all communication with the PokeAPI
- **Cache System**: Reduces API calls by caching responses for 5 minutes
- **Command Handlers**: Modular command implementations

## API Integration

This application uses the [PokeAPI](https://pokeapi.co/) to fetch Pokémon data. No authentication is required.

## Technical Details

- **Concurrency**: Thread-safe cache implementation using mutexes
- **HTTP Timeout**: 5-second timeout for API requests
- **Cache TTL**: 5-minute cache duration with automatic cleanup
- **Catch Mechanism**: Success rate based on Pokémon's base experience (higher experience = harder to catch)

## Running Tests

Execute the test suite:

```bash
go test ./...
```

## Limitations

- Caught Pokémon are stored in memory and will be lost when the application exits
- No persistent storage or save functionality
- Requires active internet connection for API access

## Contributing

Feel free to submit issues and enhancement requests!

## License

MIT License
