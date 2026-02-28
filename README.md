# custom_errors

Typed error types for password management applications using thiserror.

## Error Types

| Type | Description |
|------|-------------|
| `DBError` | Database operation errors (save, fetch, delete, etc.) |
| `EncryptionError` | Password encryption errors |
| `DecryptionError` | Password decryption errors (including wrong password) |
| `AuthError` | Authentication errors wrapping DB/Encryption/Decryption |
| `AuthGeneralError` | General auth errors (login, logout) |
| `GeneralError` | Miscellaneous errors (avatar encoding, scaling) |

## Usage

Add to your `Cargo.toml`:

```toml
[dependencies]
custom_errors = { git = "https://github.com/LucioPg/custom_errors" }
```

## Example

```rust
use custom_errors::{DBError, AuthError, DecryptionError};

// Create a database error
let db_err = DBError::new_password_save_error("Connection timeout".into());

// Wrap in AuthError
let auth_err = AuthError::DB(db_err);

// Handle decryption errors
match result {
    Err(AuthError::Decryption(DecryptionError::WrongPassword)) => {
        println!("Invalid credentials");
    }
    _ => {}
}
```

## License

MIT
