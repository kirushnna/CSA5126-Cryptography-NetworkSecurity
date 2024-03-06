def generate_dsa_keypair():
    private_key = dsa.generate_private_key(
        key_size=1024,
        backend=default_backend()
    )
    public_key = private_key.public_key()
    return private_key, public_key

def sign_message(private_key, message):
    signature = private_key.sign(
        message.encode('utf-8'),
        hashes.SHA256()
    )
    return signature
  
def verify_signature(public_key, message, signature):
    try:
        public_key.verify(
            signature,
            message.encode('utf-8'),
            hashes.SHA256()
        )
        return True
    except:
        return False

if __name__ == "__main"
    private_key, public_key = generate_dsa_keypair()
    message = "Hello, DSA!"
    signature = sign_message(private_key, message)
    is_valid = verify_signature(public_key, message, signature)
    print("Message:", message)
    print("Signature:", signature)
    print("Signature is valid:", is_valid)
