# [Polymorphism in Python]

## 💡 What I Learned
- **Polymorphism**: The ability to treat objects of different classes (e.g., `Drug`, `Vaccine`) as instances of the same general class. (異なるクラスのオブジェクトを、共通のインターフェースで統一的に扱う能力)
- **Method Overriding**: Child classes provide a specific implementation of a method that is already defined in its Parent class. (親クラスのメソッドを子クラスで上書きし、独自の振る舞いをさせる)
- **Duck Typing**: "If it walks like a duck and quacks like a duck, it must be a duck." In Python, we don't check type; we check behavior. (Pythonでは型チェックをせず、「そのメソッドを持っているか」で判断する)

## 💻 Code Snippet
```python
class Drug:
    def calculate_risk(self):
        return "Low Risk: Standard chemical analysis required."

class Vaccine(Drug):
    def calculate_risk(self):
        # Overriding with specific logic
        return "High Risk: Cold-chain integrity check required."

# The "Manager" code doesn't care about the specific type
def safety_check_process(items: list):
    for item in items:
        # Polymorphism in action:
        # The same method call works for both types!
        print(item.calculate_risk())

inventory = [Drug(), Vaccine(), Drug()]
safety_check_process(inventory)
```

## 🏥 Business Application
- Pharma:
    - Unified Workflow: Build a single pipeline to process adverse event reports (process_report()) regardless of the source (Email, Fax, Social Media, API).
    - Scalability: When a new product type (e.g., "Gene Therapy") is launched, we simply add a class with process_report(). No need to rewrite the main system code.
    - (副作用報告の受付システムにおいて、メール、FAX、SNSなど情報源が違っても、共通の処理メソッドを呼ぶだけで対応できるようにする。新しい製品カテゴリが増えても既存システムを壊さずに拡張できる。)
- Logistics:
    - Cost Calculation: A single calculate_shipping_cost() function works for AirFreight (weight-based) and OceanFreight (volume-based).
    - Tracking: A unified get_status() dashboard that handles data from diverse carriers (FedEx, DHL, Maersk) seamlessly.
    - (航空便（重量課金）と船便（容積課金）で計算ロジックが異なっていても、システム側は calculate_cost() を呼ぶだけで正しい運賃を算出できる。)