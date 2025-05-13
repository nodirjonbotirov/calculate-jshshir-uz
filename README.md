```python
def calculate_jshshir(gender, birth_date, region_code, personal_num):
    day, month, year = birth_date[:2], birth_date[2:4], birth_date[4:]
    full_year = int(f"19{year}") if int(year) >= 30 else int(f"20{year}")

    # Gender and century mapping
    gender_codes = {
        1: {1800: 1, 1900: 3, 2000: 5},  # male
        2: {1800: 2, 1900: 4, 2000: 6}   # female
    }
    century = full_year - (full_year % 100)
    gender_idx = gender_codes[gender][century]

    region_str = f"{region_code:03d}"
    personal_str = f"{personal_num:03d}"

    # Base for checksum calculation (YYMMDD order)
    checksum_base = f"{gender_idx}{year}{month}{day}{region_str}{personal_str}"
    weights = [3, 7, 1, 3, 7, 1, 3, 7, 1, 3, 7, 1, 3]
    checksum = sum(int(d) * w for d, w in zip(checksum_base, weights)) % 10

    return f"{gender_idx}{day}{month}{year}{region_str}{personal_str}{checksum if checksum != 10 else 0}"

```
