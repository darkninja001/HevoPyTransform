This repository contains **Python transformation scripts** for **Hevo Data**, helping users modify incoming data before ingestion into the destination.  

## 📌 **What This Repository Offers**  
✅ **Merge multiple source tables into a single destination table**  
✅ **Filter or rename event data before ingestion**  
✅ **Modify, drop, or rename specific fields dynamically**  
✅ **Standardize column names across different sources**  
✅ **Apply transformations to streamline data ingestion**  

---

## 🔥 **Use Cases & Examples**  

### 1️⃣ **Merge Multiple Source Tables into One**  
💡 **Scenario:** You want to combine `orders`, `customers`, and `products` into a single table (`new_common_table`).  

🔹 **Solution:**  
```python
from io.hevo.api import Event

def transform(event):
    event.rename('new_common_table')
    return event
