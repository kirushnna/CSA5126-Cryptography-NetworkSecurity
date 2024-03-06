import numpy as np
def text_to_matrix(text, n):
    text = ''.join(filter(str.isalpha, text.upper()))
    text += 'X' * (n - (len(text) % n)) if len(text) % n != 0 else ''
    return np.array([ord(char) - ord('A') for char in text]).reshape(-1, n)
def matrix_to_text(matrix):
    return ''.join([chr(val + ord('A')) for val in matrix.flatten()])
def encrypt(plaintext, key):
    plaintext_matrix = text_to_matrix(plaintext, len(key))
    key_matrix = np.array([ord(char) - ord('A') if char.isalpha() else int(char) for char in key]).reshape(len(key), -1)
    ciphertext_matrix = np.dot(key_matrix, plaintext_matrix) % 26
    return matrix_to_text(ciphertext_matrix)
def decrypt(ciphertext, key):
    key_matrix = np.array([ord(char) - ord('A') if char.isalpha() else int(char) for char in key]).reshape(len(key), -1)
    det = int(round(np.linalg.det(key_matrix))) % 26
    det_inv = pow(det, -1, 26)
    adjugate_matrix = (det_inv * np.round(det * np.linalg.inv(key_matrix)).astype(int)) % 26
    ciphertext_matrix = text_to_matrix(ciphertext, len(key))
    plaintext_matrix = np.dot(adjugate_matrix, ciphertext_matrix) % 26
    return matrix_to_text(plaintext_matrix)
key = "9457"
plaintext = "meet me at the usual place at ten rather than eight oclock"
ciphertext = encrypt(plaintext, key)
decrypted_text = decrypt(ciphertext, key)
print("Original plaintext:")
print(plaintext)
print("\nEncrypted ciphertext:")
print(ciphertext)
print("\nDecrypted plaintext:")
print(decrypted_text)
