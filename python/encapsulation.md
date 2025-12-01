# [Encapsulation in Python]

## 💡 What I Learned
- The difference between Public Attributes and Private Attributes. (Public属性とPrivate属性の違い)
- In Python, `__` (double underscore) is used to declare Private attributes. (Pythonでは `__` をつけるとPrivateになる)
- To access Private attributes safely, use **Getter and Setter methods**. (Private変数へのアクセスにはGetter/Setterを使う)

## 💻 Code Snippet
```python
class Vault:
    def __init__(self):
        # Private variable (Cannot be accessed directly like v.__secret)
        self.__secret = "1234"

    # Getter (Read-only access)
    def get_secret(self):
        return self.__secret

    # Setter (Write access with validation)
    def set_secret(self, new_secret):
        if len(new_secret) < 4:
            print("Error: Password too short!")
        else:
            self.__secret = new_secret
```

## 🏥 Business Application
- Pharma: Encapsulate sensitive data like Drug Cost Price or PII (Personally Identifiable Information) of patients to prevent unauthorized overwriting. (薬の原価や、治験の患者個人情報（PII）を隠蔽し、誤って書き換えられないようにする。)
- Logistics: Encapsulate driver's contact info or Contract Rates to protect business confidentiality. (ドライバーの連絡先や、運賃契約（Contract Rate）をカプセル化して保護する。)