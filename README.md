meniu = {
    "Pica Margarita": 7.99,
    "Pica Pepperoni": 8.99,
    "Pica Hawaii": 9.49,
    "Kola": 1.99,
    "Vanduo": 1.49
}

krepselis = []


def rodyti_meniu():
    print("\n--- MENIU ---")
    for i, (preke, kaina) in(meniu.items(), start=1):
        print(f"{i}. {preke} - {kaina:.2f} €")


def prideti_preke():
    rodyti_meniu()
    pasirinkimas = input("Įveskite prekės numerį: ")

    if not pasirinkimas.isdigit():
        print("Klaida: įveskite skaičių.")
        return

    pasirinkimas = int(pasirinkimas)

    if 1 <= pasirinkimas <= len(meniu):
        preke = list(meniu.keys())[pasirinkimas - 1]
        krepselis.append(preke)
        print(f"{preke} pridėta į krepšelį.")
    else:
        print("Tokios prekės nėra.")


def pasalinti_preke():
    if not krepselis:
        print("Krepšelis tuščias.")
        return

    rodyti_krepseli()
    pasirinkimas = input("Įveskite prekės numerį, kurią norite pašalinti: ")

    if not pasirinkimas.isdigit():
        print("Klaida: įveskite skaičių.")
        return

    pasirinkimas = int(pasirinkimas)

    if 1 <= pasirinkimas <= len(krepselis):
        preke = krepselis.pop(pasirinkimas - 1)
        print(f"{preke} pašalinta iš krepšelio.")
    else:
        print("Neteisingas pasirinkimas.")


def rodyti_krepseli():
    print("\n--- KREPŠELIS ---")
    if not krepselis:
        print("Krepšelis tuščias.")
        return

    for i, preke in(krepselis, start=1):
        print(f"{i}. {preke} - {meniu[preke]:.2f} €")

    print(f"Bendra suma: {skaiciuoti_suma():.2f} €")


def skaiciuoti_suma():
    suma = 0
    for preke in krepselis:
        suma += meniu[preke]
    return suma


def issaugoti_uzsakyma():
    if not krepselis:
        print("Nėra ką išsaugoti.")
        return

    with open("uzsakymas.txt", "w", encoding="utf-8") as failas:
        failas.write("UŽSAKYMAS:\n")
        for preke in krepselis:
            failas.write(f"{preke} - {meniu[preke]:.2f} €\n")
        failas.write(f"\nBendra suma: {skaiciuoti_suma():.2f} €")

    print("Užsakymas išsaugotas faile 'uzsakymas.txt'.")


def pagrindinis_meniu():
    while True:
        print("\n===== PAGRINDINIS MENIU =====")
        print("1. Rodyti meniu")
        print("2. Pridėti prekę")
        print("3. Pašalinti prekę")
        print("4. Peržiūrėti krepšelį")
        print("5. Išsaugoti užsakymą")
        print("0. Išeiti")

        pasirinkimas = input("Pasirinkite veiksmą: ")

        if pasirinkimas == "1":
            rodyti_meniu()
        elif pasirinkimas == "2":
            prideti_preke()
        elif pasirinkimas == "3":
            pasalinti_preke()
        elif pasirinkimas == "4":
            rodyti_krepseli()
        elif pasirinkimas == "5":
            issaugoti_uzsakyma()
        elif pasirinkimas == "0":
            print("Ačiū, kad naudojotės programa!")
            break
        else:
            print("Neteisingas pasirinkimas.")



pagrindinis_meniu()
