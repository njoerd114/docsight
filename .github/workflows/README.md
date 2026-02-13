# GitHub Actions Workflows

## Available Workflows

### 1. Tests (`tests.yml`)

**Trigger:** Push/PR to main, develop, feat/* branches

**What it does:**
- Runs full test suite on Python 3.10, 3.11, and 3.12
- Generates coverage report
- Uploads coverage to Codecov (Python 3.12 only)

**Status Badge:**
```markdown
![Tests](https://github.com/YOUR_USERNAME/docsight/workflows/Tests/badge.svg)
```

### 2. Lint (`lint.yml`)

**Trigger:** Push/PR to main, develop, feat/* branches

**What it does:**
- Checks code formatting with `black`
- Checks import sorting with `isort`
- Lints code with `flake8`
- Continues on formatting errors (non-blocking)
- Fails on syntax errors

**Status Badge:**
```markdown
![Lint](https://github.com/YOUR_USERNAME/docsight/workflows/Lint/badge.svg)
```

### 3. Driver Tests (`driver-tests.yml`)

**Trigger:** Push/PR affecting driver code

**Paths monitored:**
- `app/drivers/**`
- `tests/test_drivers.py`
- `tests/test_*_driver.py`
- `tests/test_modem_integration.py`

**What it does:**
- Runs driver interface tests
- Runs FritzBox driver tests
- Runs Vodafone driver tests
- Runs modem integration tests
- Generates driver-specific coverage report
- Uploads coverage HTML as artifact

**Status Badge:**
```markdown
![Driver Tests](https://github.com/YOUR_USERNAME/docsight/workflows/Driver%20Tests/badge.svg)
```

### 4. Docker Build (`docker.yml`)

**Trigger:** Push to main/dev, tags, manual dispatch

**What it does:**
- Builds Docker image for multiple platforms (amd64, arm64, arm/v7)
- Pushes to GitHub Container Registry
- Tags: latest, dev, version tags, SHA
- Uses build cache for faster builds

**Status Badge:**
```markdown
![Docker Build](https://github.com/YOUR_USERNAME/docsight/workflows/Build%20and%20Push%20Docker%20Image/badge.svg)
```

## Local Testing

Run the same checks locally before pushing:

```bash
# Run all tests
pytest tests/ -v

# Run with coverage
pytest tests/ --cov=app --cov-report=term-missing

# Run driver tests only
pytest tests/test_drivers.py tests/test_vodafone_driver.py tests/test_modem_integration.py -v

# Check formatting
black --check app/ tests/

# Fix formatting
black app/ tests/

# Check imports
isort --check-only app/ tests/

# Fix imports
isort app/ tests/

# Lint
flake8 app/ tests/ --max-line-length=127
```

## Coverage Reports

Coverage reports are uploaded as artifacts and can be downloaded from the Actions tab:
- **Driver Coverage**: Available for 7 days after each driver test run
- **Full Coverage**: Uploaded to Codecov (if configured)

## Adding New Workflows

To add a new workflow:

1. Create `.github/workflows/your-workflow.yml`
2. Define triggers, jobs, and steps
3. Test locally with `act` (optional): `act -j your-job-name`
4. Push and verify in Actions tab

## Workflow Status

View all workflow runs: `https://github.com/YOUR_USERNAME/docsight/actions`
