# Cache Server Benchmark Project

This project benchmarks the performance of different cache servers (Redis, Garnet, and Dragonfly) using Docker containers and C#.

## Prerequisites

- Windows OS
- Docker Desktop
- .NET SDK 9.0 or later
- Docker Compose

## Cache Servers Tested

- Redis (Latest)
- Garnet (Latest)
- Dragonfly (Latest)

## Project Structure

- `CacheBenchmark/` - C# benchmark project using BenchmarkDotNet
- `docker-compose.yml` - Docker configuration for cache servers

## How to Run

1. Start Docker containers:
```bash
docker-compose up -d
```

2. Run the benchmark:
```bash
cd CacheBenchmark
dotnet run -c Release
```

## Sample Benchmark Results

```plaintext
BenchmarkDotNet v0.14.0, Windows 11 (10.0.26100.2605)
11th Gen Intel Core i7-11800H 2.30GHz, 1 CPU, 16 logical and 8 physical cores
.NET SDK 9.0.200-preview.0.24575.35

| Method         | Mean      | Error    | StdDev   | Allocated |
|---------------|-----------|----------|-----------|-----------|
| Redis-GET     | 490.6 ms  | 10.78 ms | 6.42 ms  | 1425.91 KB|
| Redis-SET     | 531.1 ms  | 15.99 ms | 9.51 ms  | 403.16 KB |
| Garnet-SET    | 553.0 ms  | 12.60 ms | 7.50 ms  | 404.19 KB |
| Dragonfly-SET | 566.0 ms  | 10.81 ms | 6.43 ms  | 410.31 KB |
| Dragonfly-GET | 566.6 ms  | 10.98 ms | 6.53 ms  | 1435.05 KB|
| Garnet-GET    | 622.1 ms  | 10.64 ms | 6.33 ms  | 1419.39 KB|
```

## Test Configuration

- Each test performs 1000 operations
- Data size: 1KB per value
- Tests include both SET and GET operations
- All tests run with 3 iterations and 3 warmup counts

## Performance Summary

1. Redis shows the best overall performance:
   - Fastest GET operations (490.6 ms)
   - Efficient SET operations (531.1 ms)

2. Dragonfly shows consistent performance:
   - Similar timing for both GET and SET (around 566 ms)
   - Slightly higher memory allocation

3. Garnet:
   - Competitive SET performance (553.0 ms)
   - Slower GET operations (622.1 ms)
   - Efficient memory usage for SET operations

## Memory Usage

- SET operations use ~400-410 KB
- GET operations use ~1.4 MB
- Memory usage is similar across all cache servers

## License

MIT

## Contributing

Feel free to submit issues and pull requests.