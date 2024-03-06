def generate_random_key():
    return urandom(10)  
def generate_random_iv():
    return urandom(16)   
def pad_data(data):
    padder = padding.PKCS7(128).padder()
    padded_data = padder.update(data) + padder.finalize()
    return padded_data
def encrypt_cbc_aes(data, key, iv):
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    encryptor = cipher.encryptor()
    encrypted_data = encryptor.update(pad_data(data)) + encryptor.finalize()
    return encrypted_data
def decrypt_cbc_aes(encrypted_data, key, iv):
    cipher = Cipher(algorithms.AES(key), modes.CBC(iv), backend=default_backend())
    decryptor = cipher.decryptor()
    decrypted_data = decryptor.update(encrypted_data) + decryptor.finalize()
    return decrypted_data
if __name__ == "__main__":
    plaintext = b"This is a secret message."
    key = generate_random_key()
    iv = generate_random_iv()
    ciphertext = encrypt_cbc_aes(plaintext, key, iv)
    decrypted_text = decrypt_cbc_aes(ciphertext, key, iv)
    print("Original plaintext:", plaintext)
    print("Encrypted ciphertext:", ciphertext)
    print("Decrypted plaintext:", decrypted_text)
