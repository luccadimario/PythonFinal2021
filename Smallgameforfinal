import sys
import time
import random
def search_string_in_file(file_name, string_to_search):
    line_number = 0
    list_of_results = []
    # Open the file in read mode
    with open(file_name, 'r') as read_obj:
        # Read all lines in file
        for line in read_obj:
            # For each line, check if line contains the string
            line_number += 1
            if string_to_search in line:
                # If yes, then add the line number & line to the list
                list_of_results.append((line_number, line.rstrip()))
    # Return list of tuples containing line numbers and lines where the string is found
    return list_of_results

def newgame(): # lists and has the user enter class as well as name for their character
  barbarianstat = "10 10 2"
  wizardstat = "12 8 2"
  print("Here are the stats for barbarian, Attack, Health, Heal", barbarianstat)
  print("Here are the stats for wizard, Attack, Health, Heal", wizardstat)
  gameclass = input("What class do you want your character to be? This will change your options for attacking. The choices are Wizard or Barbarian.")
  charname = input("Enter a one word name for your character: ")
  print("Great! Good luck,",charname)
  if gameclass.upper() == "BARBARIAN": #writes choices/name/class/stats to file
    save = open('savefile', 'a')
    save.write(charname.upper() + " ")
    save.write(gameclass.upper() + " ")
    for num in barbarianstat:
        save.write(num)
    save.write(" "+"1")
    save.write(" " + "0")
    save.write(" " + "0" + "\n")
    save.close()
  else:
    save = open('savefile', 'a')
    save.write(charname.upper() + " ")
    save.write(gameclass.upper() + " ")
    for num in wizardstat:
        save.write(num)
    save.write(" "+"1")
    save.write(" " + "0")
    save.write(" " + "0" + "\n")
    save.close()
  game(charname)
def game(name):#actual game file
  enemieslst = ['Warlock','Gremlin','Enemy Swordsman','Ogre']
  filelines = search_string_in_file('savefile',str(name.upper()))
  for elem in filelines:
    linenum = elem[0]
  print(filelines)
  values = str(filelines).split()#takes the stats from file and loads them into variables
  gameclass = values[2]
  attack = values[3]
  health = values[4]
  heal = values[5]
  level = values[6]
  xp = values[7]
  print("Welcome",name)
  print("Here is the dummy where we will show you how to (a)ttack or (h)eal") #Demo
  print("after every attack or heal an amount of health will be taken from you as the enemy will fight back.")
  print("You can attack to do damage to the enemy or you can heal to heal back some health.")
  time.sleep(1)
  print("/////////////////////////////")
  print("//////////____///////////////")
  print("/////////(0//0)//////////////")
  print("/////////(\__/)//////////////")
  print("//////////(||)////////////////")
  print("//////====(||)=====///////////")
  print("//////////(//)///////////////")
  print("//////////0///0///////////////")
  print("/////////0/////0//////////////")
  print("////////0///////0/////////////")
  print("///////0/////////0////////////")
  dummyhealth = 5
  battlehealth = int(health)
  dummydamage = 1
  while dummyhealth > 0:
      choice = input("type (a) to attack or (h) to heal: ") #choice to attack or heal
      if choice.upper() == "A":
          dummyhealth -= int(attack)
      elif choice.upper() == "H":
          if battlehealth == int(health):
              print("You are already at max health! Your max health will go up after you level up.")
          else:
              battlehealth += int(heal)
      if dummyhealth > 0: #handles finishing the battle if dumy loses all health
        print("You took",dummydamage,"damage!")
        battlehealth -= int(dummydamage)
        print("Attacker health:",dummyhealth,"Your health:", battlehealth )
      else:
        continue
  print("Good job, you beat him! You finished with",battlehealth,"health! You're ready!")
  battlehealth = int(health)
  time.sleep(1)
  print("From now on enemies will scale with level, between battles you will be healed with max health.")
  time.sleep(1)
  print("STAY ALIVE! If you die the game will end and you will have to create a new character!")
  time.sleep(1)
  print("When you kill an enemy it will drop a random amount of XP which you can gain to level up increasing your damage, heal, and health.")
  yndone = "YES"
  while yndone.upper() == "YES": #makes sure user can stop when they want
     randomgen = random.randint(0,3)
     healthofenemy = int(level)*1.15*10
     damageofenemy = int(health)/random.randint(2,4) #calculates some values of the enemy as well as name. Values like damage and health vary upon what level the user is
     enemydamage = int(damageofenemy)
     enemyhealth = int(healthofenemy)
     enemy = enemieslst[randomgen]
     battlehealth = int(health)
     print("You've encountered a(n)", enemy,"!")
     while enemyhealth > 0: #makes sure enemy is not dead
         choice = input("type a for attack or h for heal: ")
         if choice.upper() == "A":#attack choice
             enemyhealth -= int(attack)
         elif choice.upper() == "H":
             if battlehealth == int(health):#heal choice
                 print("You are already at max health! Your max health will go up after you level up.")
             else:
                 battlehealth += int(heal)
         else:
            continue
         if enemyhealth > 0:#handles damage of user and enemy
             print("You took", enemydamage, "damage!")
             battlehealth -= int(enemydamage)
             print("Attacker health:", enemyhealth, "Your health:", battlehealth)
             if battlehealth <= 0: #FIX
               infile = open('savefile','r').readlines() #removes game file of player if they die
               with open('savefile','w') as outfile:
                for index,line in enumerate(infile):
                  if index != (int(linenum) - 1):
                    outfile.write(line)
                outfile.write("\n")

               sys.exit("You Died, Game Over")#ends program
             else:
               continue
         else:
             battlehealth = int(health)
             break
     print("You've defeated the",enemy,)#handles XP gain and leveling up
     xp = int(float(xp))
     level = int(float(level))
     attack = int(float(attack))
     health = int(float(attack))
     heal = int(float(heal))
     XPdropped = random.randint(1,10)
     print("The enemy dropped",XPdropped,"XP")
     xp += (XPdropped)
     level = int(float(level))
     if xp > 10:
        print("Congrats youve leveled up!")
        remainder = int(xp) % 10 #this changes the players stats when they level up
        level += 1
        xp = 0 + int(remainder)
        attack += 2
        health += 2
        heal += 1
        time.sleep(2)
        yndone = input("Would you like to keep playing? Yes or No: ")#makes sure they want to keep playing before loading the new enemy
        print("Ok!")
     else:
        time.sleep(2)
        yndone = input("Would you like to keep playing? Yes or No: ")
        print("Ok!")
  print("You can come back any time with your name and resume where you were!")
  infile = open('savefile','r').readlines() #removes previous save file stats
  with open('savefile','w') as outfile:
    for index,line in enumerate(infile):
      if index != (int(linenum) - 1):
        outfile.write(line)
    outfile.write("\n")
  save = open('savefile', 'a') #writes updated stats to the save file
  save.write(name.upper() + " ")
  save.write(gameclass.upper() + " ")
  save.write(str(attack) + " ")
  save.write(str(health) + " ")
  save.write(str(heal) + " ")
  save.write(str(level) + " ")
  save.write(str(xp) + " ")
  save.write('0' + "\n")
  save.close()


#This is the main program that just handles checking for game file and asking to start the game as well as running functions for the game itself
yn = input("Would you like to play the best text based fighter in existance? Type yes or no: ")
if yn.upper() == "YES":
  ynsave = input("Do you already have a save file from previously? Type yes or no: ")
  if ynsave.upper() == "YES":
    name = input("Please enter the name of your previous character: ")
    lines = search_string_in_file('savefile',name.upper()) #searches for name in save file
    if len(lines) > 0: # if it is in the file the lines that it is found in will be greater than 0
      print("Ok I found the game file, here we go.")
      game(name)
    else:
      newgameyn = input("I do not see a save file, would you like to start a new game? Type Yes or No: ")
      if newgameyn.upper() == "YES":#runs function to set up new character
        print("Ok here we go.")
        newgame()
      else:
        sys.exit("Ok but you're missing out!") #if they dont want to play it ends the program
  else:
    print("Ok, we will set you up with a new character!")#runs function to set up new character
    newgame()
else:
  sys.exit("Ok but you're missing out!")#if they dont want to play it ends the program
