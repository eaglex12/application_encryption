# Encryption Service

This is a simple encryption service built with NestJS that provides methods to securely encrypt and decrypt data using AES-256-CBC encryption.

## Features

- AES-256-CBC encryption algorithm
- Dynamic initialization vector (IV) for each encryption
- Secure handling of encryption keys
- Error handling during decryption

## Installation

To use the `EncryptionService`, ensure you have a NestJS project set up. Then, add the `EncryptionService` to your module.

```bash
npm install --save @nestjs/common
```

## Configuration

Before using the `EncryptionService`, set the encryption key in your environment variables. The key should be a 64-character hexadecimal string representing a 32-byte key.

```plaintext
ENCRYPTION_KEY=<your-64-character-hexadecimal-key>
```

## Usage

### Importing the Service

Import the `EncryptionService` in your desired module.

```typescript
import { Module } from "@nestjs/common";
import { EncryptionService } from "./encryption.service";

@Module({
	providers: [EncryptionService],
	exports: [EncryptionService],
})
export class AppModule {}
```

### Encrypting Data

You can encrypt data by calling the `encrypt` method, which returns an object containing the IV and the encrypted data.

```typescript
import { EncryptionService } from "./encryption.service";

@Injectable()
export class SomeService {
	constructor(private readonly encryptionService: EncryptionService) {}

	encryptData(text: string) {
		const { iv, encryptedData } = this.encryptionService.encrypt(text);
		// Use the IV and encrypted data as needed
	}
}
```

### Decrypting Data

To decrypt data, use the `decrypt` method. You'll need to provide the IV and the encrypted data.

```typescript
import { EncryptionService } from "./encryption.service";

@Injectable()
export class SomeService {
	constructor(private readonly encryptionService: EncryptionService) {}

	decryptData(iv: string, encryptedData: string) {
		try {
			const decryptedText = this.encryptionService.decrypt(iv, encryptedData);
			// Use the decrypted text as needed
		} catch (error) {
			console.error("Decryption failed:", error.message);
			// Handle the error appropriately
		}
	}
}
```

## Error Handling

The `decrypt` method includes error handling to ensure that invalid inputs do not cause unhandled exceptions. If decryption fails, it will log the error message and throw a new error with a user-friendly message.

## Important Notes

- Always store your encryption key securely and never hard-code it in your application.
- Ensure that the IV is unique for each encryption operation to maintain the security of your data.
- This service is suitable for basic encryption needs but may require additional security measures for highly sensitive information.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
