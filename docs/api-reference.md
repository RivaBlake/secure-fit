# Secure Fit Coding Practice System - API Reference

## Smart Contract Functions

### Core Functions

#### `addEntry(externalEuint32 encryptedMinutes, externalEuint32 encryptedProblems, externalEuint32 encryptedSuccesses, externalEuint32 encryptedFailures, bytes inputProof)`
Add a new practice entry with encrypted data.
- **Parameters:**
  - `encryptedMinutes`: Encrypted minutes spent coding
  - `encryptedProblems`: Encrypted number of problems solved
  - `encryptedSuccesses`: Encrypted number of successful attempts
  - `encryptedFailures`: Encrypted number of failed attempts
  - `inputProof`: FHE input proof for all encrypted values

#### `batchAddEntries(externalEuint32[] encryptedMinutesArray, externalEuint32[] encryptedProblemsArray, externalEuint32[] encryptedSuccessesArray, externalEuint32[] encryptedFailuresArray, bytes inputProof)`
Add multiple practice entries in a single transaction.
- **Parameters:**
  - Arrays of encrypted values for batch processing
  - Single input proof for all entries
  - Maximum 10 entries per batch

### Statistics Functions

#### `getTotalMinutes(address user)`
Get encrypted total minutes for a user.
- **Returns:** Encrypted total minutes

#### `getTotalProblems(address user)`
Get encrypted total problems for a user.
- **Returns:** Encrypted total problems

#### `getTotalSuccesses(address user)`
Get encrypted total successes for a user.
- **Returns:** Encrypted total successes

#### `getTotalFailures(address user)`
Get encrypted total failures for a user.
- **Returns:** Encrypted total failures

#### `getTotalAttempts(address user)`
Get encrypted total attempts for a user.
- **Returns:** Encrypted total attempts

#### `getPassRateNumerator(address user)`
Get encrypted pass rate numerator (successes * 100) for a user.
- **Returns:** Encrypted pass rate numerator

#### `getPracticeStatistics(address user)`
Get comprehensive practice statistics.
- **Returns:** `(totalEntries, averageMinutes, averageProblems)`

### Utility Functions

#### `getEntryCount(address user)`
Get total number of practice entries for a user.
- **Returns:** Entry count

#### `getEntry(address user, uint256 index)`
Get a specific practice entry by index.
- **Returns:** `(timestamp, encryptedMinutes, encryptedProblems, encryptedSuccesses, encryptedFailures)`

## Practice Entry Structure

```solidity
struct PracticeEntry {
    uint256 timestamp;        // Entry creation timestamp
    euint32 codingMinutes;    // Encrypted minutes spent coding
    euint32 problems;         // Encrypted problems solved
    euint32 successes;        // Encrypted successful attempts
    euint32 failures;         // Encrypted failed attempts
}
```

## Security Features

- **FHE Encryption**: All practice data is fully homomorphically encrypted
- **Private Analytics**: Statistics computation happens on encrypted data
- **Zero-Knowledge**: No plaintext data is ever stored or revealed
- **Secure Decryption**: Users can only decrypt their own data with proper permissions

## Error Handling

- Invalid proof verification
- Array length mismatches in batch operations
- Access control violations
- Gas limit exceeded for large batches
