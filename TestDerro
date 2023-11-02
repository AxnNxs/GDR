
from threading import Event
import keyboard
import secrets
import time
import sys


'''
Questa classe (ahah) costruisce tutti i valori che servono per ogni guerriero:
- nome classe
- dado 1
- dado 2
'''
class warriorClass:

    # default constructor
    def __init__(self):
        self.name = ""
        self.dice1 = 0
        self.dice2 = 0

    # un metodo per stampare tutti i dati del combattente
    def get_data_warrior(self):
        print("\nnome classe: " + str(self.name))
        print("1° dado: 1d" + str(self.dice1))
        print("2° dado: 1d" + str(self.dice2))

    # ritorna il nome della classe del combattente
    def get_class(self):
        n = "nome classe: " + str(self.name)
        return n

    # ritorna il 1° dado attacco utilizzato dal combattente
    def get_dice1(self):
        v = "1° dado: 1d" + str(self.dice1)
        return v

    # ritorna il 2° dado attacco utilizzato dal combattente
    def get_dice2(self):
        v = "2° dado: 1d" + str(self.dice2)
        return v


# altri metodi

def insert_values():
    diceList = [2,4,6,8,10,12,20,100]
    classe = input("Inserisci ora il nome della tua classe: ")
    d1 = input("Inserisci ora il 1° dado di attacco. Specifica solo il numero, per esempio: per avere 1d6 digita solo 6): ")
    while (int(d1) not in diceList):
        d1 = input("Eddai, famo i seri, sto dado non esiste... metti quello giusto va: ")
    d2 = input("Inserisci ora il 2° dado di attacco. Specifica solo il numero, per esempio: per avere 1d6 digita solo 6): ")
    while (int(d2) not in diceList):
        d2 = input("Ao che stai a giocà, sto dado non esiste... metti quello giusto va: ")
    return (classe, d1, d2)

def insert_values_auto(list):
    soldato = warriorClass()
    scout = warriorClass()
    selvaggio = warriorClass()
    soldato.name = str('Soldato')
    soldato.dice1 = int(6)
    soldato.dice2 = int(6)
    scout.name = str('Scout')
    scout.dice1 = int(6)
    scout.dice2 = int(4)
    selvaggio.name = str('Selvaggio')
    selvaggio.dice1 = int(8)
    selvaggio.dice2 = int(6)
    list.append(soldato)
    list.append(scout)
    list.append(selvaggio)
    return list

def dice_throw(dice):
    listValues = []
    for i in range(1, dice + 1):
        listValues.append(i)
    val = secrets.choice(listValues)
    return val




### Testing
def main():
    warriorList = []
    c = False
    n = 0       # n coppie di lanci
    s = 0       # s soglia per colpire
    skip = False
    skills = []
    print("Ciao Derro! Benvenuto al tuo simulatore di probabilità di quartiere!\n")
    warrior = warriorClass()

    user_input = input("Se vuoi skippare le impostazioni manuali e partire con un preset, premi t.\nAltrimenti premi qualsiasi altro tasto: ")
    if user_input.lower() == 't':
        skip = True
        insert_values_auto(warriorList)
        s = 3
        n = 1000
        print("Test in fase di avvio. Il programma ha selezionato i seguenti parametri:")
        for i in warriorList:
            i.get_data_warrior()
        skills.append('scout')
        skills.append('selvaggio')
        skills.append('soldato')
        print("\nNumero di attacchi per combattente:      " + str(n))
        print("Soglia da superare per attacco a segno:  " + str(s))
        print("Skill abilitate per: ")
        for i in skills:
            if str(i).lower() == 'scout':
                print('  ' + str(i) + ':         Danno Critico')
            if str(i).lower() == 'selvaggio':
                print('  ' + str(i) + ':     Malus 6+')
            if str(i).lower() == 'soldato':
                print('  ' + str(i) + ':       Doppio')

    while (c != True and skip == False):
        warrior = warriorClass()
        classe, d1, d2 = insert_values()

        warrior.name = str(classe)
        warrior.dice1 = int(d1)
        warrior.dice2 = int(d2)
        warriorList.append(warrior)
        user_input = input("Vuoi abilitare Dado Esplosivo per questa classe? (Digita y/n) ")
        if user_input.lower() == "y":
            print("Ok, considererò questa skill in fase di testing per il " + str(warrior.name) + '...')
        else:
            continue

        user_input = input("Vuoi aggiungere un'altra classe? (Digita y/n) ")
        
        if user_input.lower() == "y":
            print("Ok, generazione di una nuova classe...")
        else:
            c = True
            #print("Exiting...\n")
    
    c = False
    while ((c != True or n == 0 or str(n).isalpha()) and skip == False):
        n = input("Quanti attacchi vuoi effettuare? Inserisci un numero: ")
        try:
            n = int(n)
            c = True
        except: 
            print("Un numero, suvvia... : ")
    
    c = False
    while ((c != True or s == 0 or str(s).isalpha()) and skip == False):
        s = input("Qual è la soglia per colpire? Inserisci un numero: ")
        try:
            s = int(s)
            c = True
        except: 
            print("Un numero Derro! UN NUMERO! : ")


    count = 10

    def handle_keypress(key):
        print(key + " premuto, stop al countdown.")
        e.wait(timeout = 1.0)
        e.set()

    k = keyboard.add_hotkey("q", lambda: handle_keypress("q"))
    e = Event()
    print("\nTest in partenza tra " + str(count) + ' secondi.\nPremi Q per saltare il countdown.')
    while (count >= 1) and (e.is_set() == False):
        print(str(count), end = "... ", flush = True)
        e.wait(timeout = 1.0)
        count -= 1

        
    print('\n\n         Link Start!\n')
    time.sleep(1.0)

    ListAllWarriors = []
    for i in range(0, len(warriorList)):
        warrior = warriorList[i]
        dictWarrior = {warrior.name:[]}
        win_soglia = 0
        dan_tot = 0
        dan_pur = 0
        skill_count = 0
        explosions =  0
        for j in range(1, n + 1):
            explosion1 = 0
            explosion2 = 0
            listAttacks = []
            result1 = dice_throw(int(warrior.dice1))
            result2 = dice_throw(int(warrior.dice2))
            print('Attacco numero ' + str(j) + ' di ' + str(warrior.name) + '\n')
            print('Lancio il ' + str(warrior.get_dice1()) + '. Risultato: ' + str(result1))
            print('Lancio il ' + str(warrior.get_dice2()) + '. Risultato: ' + str(result2))
            if result1 == warrior.dice1:
                result = dice_throw(int(warrior.dice1))
                result1 += result
                explosion1 += 1
                print('EEEEEEEXPLOSIOOOON (cit. una certa maga kawaii, comunque ha crittato il ciotto Derrone)')
                print('Rilancio il ' + str(warrior.get_dice1()) + '. Risultato: ' + str(result) + ', Somma: ' + str(result1))
            if result2 == warrior.dice2:
                result = dice_throw(int(warrior.dice1))
                result2 += result 
                explosion2 += 1
                print('EEEEEEEXPLOSIOOOON (cit. una certa maga kawaii, comunque ha crittato il gnappetto Derruccio)')
                print('Rilancio il ' + str(warrior.get_dice2()) + '. Risultato: ' + str(result) + ', Somma: ' + str(result2))
            explosions += (explosion1 + explosion2)
            listAttacks.append(result1)
            listAttacks.append(result2)
            throwmax = max(listAttacks)
            throwmin = min(listAttacks)
            if (throwmax == result1):
                print("\nIl dado usato per verificare il successo dell'attacco è il    d" + str(warrior.dice1) + '')
            else:
                print("\nIl dado usato per verificare il successo dell'attacco è il    d" + str(warrior.dice2) + '')
            print('Il combattente colpisce solo se   ------------>               ' + str(throwmax) + ' >= ' + str(s) + '?')
            if throwmax >= s:
                print('Il colpo è andato a segno DERRO! ENNAMO EDDAJE EDDERRO!')
                win_soglia += 1
                dan_max = throwmax + throwmin
                dan_pur += dan_max
                if (str(warrior.name)).lower() in skills and (str(warrior.name)).lower() == 'scout':    # Danno Critico
                    skill_count += 1
                    explosivemin = min(listAttacks)*2
                    print("     Danno Critico: il risultato dell'altro dado raddoppia!   " + str(throwmin) + ' --x2--> ' + str(explosivemin))
                    dan_max += throwmin
                if (str(warrior.name)).lower() in skills and (str(warrior.name)).lower() == 'selvaggio' and (result1 >= 6): # Malus 6+
                    skill_count += 1
                    print("     Malus 6+:   sottraggo 1 al danno totale.")
                    dan_max -= 1
                if (str(warrior.name)).lower() in skills and (str(warrior.name)).lower() == 'soldato' and (result1 == result2): # Malus 6+
                    skill_count += 1
                    print("     Doppio:   raddoppio la somma!")
                    dan_max += throwmax + throwmin
                print("     Il danno sferrato ammonta in totale a:                   " + str(dan_max))
                dan_tot += dan_max
                
            else:
                print('Derro, Derro... questo è intelligente ma non si applica... ')
            dictWarrior[warrior.name].append(listAttacks)
            print('------------------------------------------------------------------------------')
        dictWarrior.update({'Vittorie' : win_soglia})
        dictWarrior.update({'Danni inflitti' : dan_tot})
        dictWarrior.update({'Danni senza Skill' : dan_pur})
        dictWarrior.update({'Skill utilizzate' : skill_count})
        dictWarrior.update({'Dadi esplosi' : explosions})
        ListAllWarriors.append(dictWarrior)
        print("\nCiclo di Test finito per il combattente " + str(warrior.name) + '...')
        time.sleep(1.0)
    
    print("Il Test è finito. Pubblicazione dei risultati in corso...\n")
    time.sleep(1.0)
    
    #print(ListAllWarriors)     #for testing purposes
    for i in ListAllWarriors:
        vin = 0
        dan = 0
        nam = ''
        for j in i:
            if (j != 'Vittorie' and j != 'Danni inflitti' and j != 'Skill utilizzate' and j != 'Danni senza Skill' and j != 'Dadi esplosi'):
                nam = j
                print('Il combattente ' + str(j), end = "")
            elif (j != 'Danni inflitti' and j != 'Skill utilizzate' and j != 'Danni senza Skill' and j != 'Dadi esplosi'):
                vin = i[j]
                print(' ha un numero di ' + str(j) + ' pari a ' + str(i[j]) + ' su ' + str(n) + ' attacchi.' +
                      '\nCiò vuol dire che ha una Probabilità di attacco a segno del            ' + str(round(((i[j]/n)*100), 2)) + '%')
            elif (j != 'Skill utilizzate' and j != 'Danni senza Skill' and j != 'Dadi esplosi'):
                dan = i[j]
                print(str(j) + ' in media sul numero di Attacchi (DPA):                  ' + str(round(i[j]/n, 2)))
            elif (j != 'Danni senza Skill' and j != 'Dadi esplosi'):
                print('Occasioni di ' + str(j) + ':                                         ' + str(i[j]))
            elif  j != 'Dadi esplosi':
                print(str(j) + ' in media sul numero di attacchi (DPA NS):            ' + str(round(i[j]/n, 2)))
            else:
                print(str(j) + ' in media sul numero di Attacchi (ExPA):                   ' + str(round((i[j]/n)*10, 1)) + '/10')
        print("Danni inflitti in media sul numero di Vittorie (DPV):                  " + str(round((dan/vin), 2)) + '\n')
    print('\n')
    return







if __name__ == "__main__":
    try:
        main()
    except BaseException:
        import sys
        print(sys.exc_info()[0])
        import traceback
        print(traceback.format_exc())
    finally:
        print("Premi Enter per uscire ...")
        input()
