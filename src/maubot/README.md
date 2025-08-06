# 🤖 Maubot Service

A modular Docker Compose configuration system for Maubot with support for multiple environments and extensions.

## 🏗️ Project Structure

```sh
src/maubot/
├── components/                              # Source compose components
│   ├── base/                               # Base components
│   │   ├── docker-compose.yml              # Main Maubot service
│   │   └── .env.example                    # Base environment variables
│   ├── environments/                       # Environment components
│   │   ├── devcontainer/
│   │   │   └── docker-compose.yml          # Dev container integration
│   │   ├── forwarding/
│   │   │   └── docker-compose.yml          # Development with port forwarding
│   │   ├── letsencrypt/
│   │   │   ├── docker-compose.yml          # Let's Encrypt SSL
│   │   │   └── .env.example                # Let's Encrypt variables
│   │   └── step-ca/
│   │       ├── docker-compose.yml          # Step CA SSL
│   │       └── .env.example                # Step CA variables
│   └── extensions/                         # Extension components
│       ├── step-ca-trust/                  # Step CA trust extension
│       │   ├── docker-compose.yml          # Step CA trust configuration
│       │   └── .env.example                # Step CA trust variables
│       └── .gitkeep                        # Placeholder for future extensions
├── build/                        # Generated configurations (auto-generated)
│   ├── devcontainer/
│   │   ├── base/                 # Dev container + base configuration
│   │   └── step-ca-trust/        # Dev container + step-ca-trust extension
│   ├── forwarding/
│   │   ├── base/                 # Development + base configuration
│   │   └── step-ca-trust/        # Development + step-ca-trust extension
│   ├── letsencrypt/
│   │   ├── base/                 # Let's Encrypt + base configuration
│   │   └── step-ca-trust/        # Let's Encrypt + step-ca-trust extension
│   └── step-ca/
│       ├── base/                 # Step CA + base configuration
│       └── step-ca-trust/        # Step CA + step-ca-trust extension
├── build.sh                      # Build script
└── README.md                     # This file
```

## 🚀 Quick Start

### 1. Build Configurations

Run the build script to generate all possible combinations:

```bash
./build.sh
```

This will create all combinations in the `build/` directory.

### 2. Choose Your Configuration

Navigate to the desired configuration directory:

```bash
# For development with port forwarding
cd build/forwarding/base/

# For development with Step CA trust
cd build/forwarding/step-ca-trust/

# For production with Let's Encrypt SSL
cd build/letsencrypt/base/

# For production with Let's Encrypt SSL and Step CA trust
cd build/letsencrypt/step-ca-trust/

# For production with Step CA SSL
cd build/step-ca/base/

# For production with Step CA SSL and trust
cd build/step-ca/step-ca-trust/

# For dev container integration
cd build/devcontainer/base/

# For dev container with Step CA trust
cd build/devcontainer/step-ca-trust/
```

### 3. Configure Environment

Copy and edit the environment file:

```bash
cp .env.example .env
# Edit .env with your values
```

### 4. Deploy

Start the services:

```bash
docker-compose up -d
```

Access: `http://localhost:29316` (for forwarding mode)

## 🔧 Available Configurations

### Environments

- **devcontainer**: Dev container integration for VS Code
- **forwarding**: Development environment with port forwarding (29316)
- **letsencrypt**: Production with Let's Encrypt SSL certificates
- **step-ca**: Production with Step CA SSL certificates

### Extensions

- **step-ca-trust**: Automatic installation of Step CA certificates as trusted for the container

### Generated Combinations

Each environment can be combined with any extension:

- `devcontainer/base` - Dev container integration
- `devcontainer/step-ca-trust` - Dev container with Step CA trust
- `forwarding/base` - Development with port forwarding
- `forwarding/step-ca-trust` - Development with Step CA trust
- `letsencrypt/base` - Production with Let's Encrypt SSL
- `letsencrypt/step-ca-trust` - Production with Let's Encrypt SSL and Step CA trust
- `step-ca/base` - Production with Step CA SSL
- `step-ca/step-ca-trust` - Production with Step CA SSL and trust

## 🔧 Environment Variables

### Base Configuration

- `COMPOSE_PROJECT_NAME`: Project name for Docker Compose (default: maubot)
- `MAUBOT_DB_FOLDER`: Data folder path (default: /data)
- `MAUBOT_PUBLIC_URL`: Public URL for Maubot
- `MAUBOT_UI_BASE_PATH`: Base path for UI (default: /_matrix/maubot)
- `MAUBOT_PLUGIN_BASE_PATH`: Base path for plugins
- `MAUBOT_UNSHARED_SECRET`: Secret key for Maubot

### Matrix Homeserver Configuration

- `MAUBOT_HOMESERVER_NAME`: Homeserver name
- `MAUBOT_HOMESERVER_URL`: Homeserver URL
- `MAUBOT_HOMESERVER_SECRET`: Application service registration secret

### Admin Configuration

- `MAUBOT_ADMIN_USERNAME`: Admin username
- `MAUBOT_ADMIN_PASSWORD`: Admin password

### Let's Encrypt Configuration

- `VIRTUAL_PORT`: Port for nginx-proxy (default: 29316)
- `VIRTUAL_HOST`: Domain for nginx-proxy
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

### Step CA Configuration

- `VIRTUAL_PORT`: Port for nginx-proxy (default: 29316)
- `VIRTUAL_HOST`: Domain for nginx-proxy
- `LETSENCRYPT_HOST`: Domain for SSL certificate
- `LETSENCRYPT_EMAIL`: Email for certificate registration

### Step CA Trust Extension

- `STEP_CA_TRUST`: Enable automatic Step CA certificate trust (default: true)
- `STEP_CA_TRUST_RESTART`: Restart container after trust installation (default: true)

## 🤖 Using Maubot

### Accessing Web Interface

```bash
# For forwarding mode
http://localhost:29316

# For SSL modes
https://your-domain.com/_matrix/maubot
```

### Managing Bots

1. Log in to the web interface with admin credentials
2. Upload plugins through the interface
3. Create bot instances
4. Configure Matrix clients for bots

### Installing Plugins

Plugins can be uploaded through the web interface or placed in the `/data/plugins` directory.

## 🛠️ Development

### Adding New Environments

1. Create directory in `components/environments/` with `docker-compose.yml` and optional `.env.example` file
2. Run `./build.sh` to generate new combinations

### File Naming Convention

All component files follow the standard Docker Compose naming convention (`docker-compose.yml`) for:

- **VS Code compatibility**: Full support for Docker Compose language features and IntelliSense
- **IDE integration**: Proper syntax highlighting and validation in all major editors
- **Tool compatibility**: Works with Docker Compose plugins and extensions
- **Standard compliance**: Follows official Docker Compose file naming patterns

### Modifying Existing Components

1. Edit the component files in `components/`
2. Run `./build.sh` to regenerate configurations
3. The `build/` directory will be completely recreated

## 🌐 Networks

- **Development**: `maubot-network` (internal)
- **Dev container**: `matrix-bridges-workspace-network` (external)
- **Let's Encrypt**: `letsencrypt-network` (external)
- **Step CA**: `step-ca-network` (external)

## 🔒 Security

⚠️ **Production Checklist:**

- Change default admin password
- Use strong passwords for authentication
- Configure firewall rules
- Regular security updates
- Set proper homeserver secrets

## 🆘 Troubleshooting

**Build Issues:**

- Ensure `yq` is installed: <https://github.com/mikefarah/yq#install>
- Check component file syntax
- Verify all required files exist

**Matrix Connection Issues:**

- Check homeserver URL correctness
- Ensure homeserver secret is correct
- Verify service accessibility: `docker logs maubot`

**SSL Issues:**

- **Let's Encrypt**: Verify domain DNS and letsencrypt-manager
- **Step CA**: Check step-ca-manager and virtual network config

**Plugin Issues:**

- Ensure plugins are compatible with Maubot version
- Check container logs for plugin loading errors
- Verify plugins directory is writable

## 📝 Notes

- The `build/` directory is automatically generated and should not be edited manually
- Environment variables in generated files use `$VARIABLE_NAME` format for proper interpolation
- Each generated configuration includes a complete `docker-compose.yml` and `.env.example`
- Missing `.env.*` files for components are handled gracefully by the build script

## 🔄 Migration from Legacy Deploy Script

The legacy `deploy.sh` script is still available for compatibility, but the new build system is recommended:

**Legacy approach:**

```bash
./deploy.sh --production --letsencrypt
```

**New approach:**

```bash
./build.sh
cd build/letsencrypt/base/
cp .env.example .env
docker-compose up -d
```

## 📚 Additional Resources

- [Official Maubot Documentation](https://docs.mau.fi/maubot/)
- [Maubot Plugin Repository](https://github.com/maubot)
- [Matrix.org Documentation](https://matrix.org/docs/)
