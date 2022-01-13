# LAB 4

Na ovoj vježbi upoznat ćemo se sa metodama zaštite podataka prilikom njihove pohrane.

Pet različitih hash funkcija pokrenit ćemo nad istim skupom podataka 100 puta te pomoću prosjećnog vremena izvođenja funkcije usporediti utjecaj prosječnog vremena izvođenja pojedine funkcije na sigurnost podataka u slučaju brute-force napada.

[Untitled](https://www.notion.so/ec074535c6294e98b8e0d6d35ec788e4)

Zaključujemo da što više iterativnih heširanja primjenimo nad istim podatkom to će brute forceanje datih podataka biti teže.

Za potrebe vježbe koristimo slijedeći kod:

```
if __name__ == "__main__":
    ITERATIONS = 100
    password = b"super secret password"

    MEMORY_HARD_TESTS = []
    LOW_MEMORY_TESTS = []

    TESTS = [
        {
            "name": "AES",
            "service": lambda: aes(measure=True)
        },
        {
            "name": "HASH_MD5",
            "service": lambda: sha512(password, measure=True)
        },
        {
            "name": "HASH_SHA256",
            "service": lambda: sha512(password, measure=True)
        }
    ]

    table = PrettyTable()
    column_1 = "Function"
    column_2 = f"Avg. Time ({ITERATIONS} runs)"
    table.field_names = [column_1, column_2]
    table.align[column_1] = "l"
    table.align[column_2] = "c"
    table.sortby = column_2

    for test in TESTS:
        name = test.get("name")
        service = test.get("service")

        total_time = 0
        for iteration in range(0, ITERATIONS):
            print(f"Testing {name:>6} {iteration}/{ITERATIONS}", end="\r")
            _, execution_time = service()
            total_time += execution_time
        average_time = round(total_time/ITERATIONS, 6)
        table.add_row([name, average_time])
        print(f"{table}\n\n")
```