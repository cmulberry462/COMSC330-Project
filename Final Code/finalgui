import math
import matplotlib.pyplot as plt
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
import os
import pandas as pd
from pandastable import *
from PIL import Image, ImageTk
from tkinter import *
import tkinter as tk
from tkinter import filedialog
from tkinter import ttk

# this code is so change the settings of pandas so when the output file is produced python does not truncate it
pd.set_option('display.max_rows', None)
pd.set_option('display.max_columns', None)
pd.set_option('display.width', None)

#Defining variables
directoryName = "";
selectedFile = "";
directory = "";

group_dfs = {}
section_dfs = {}
grade_dfs = {}

guistack = []

num_A_section       = 0;
num_Aminus_section  = 0;
num_Bplus_section   = 0;
num_B_section       = 0;
num_Bminus_section  = 0;
num_Cplus_section   = 0;
num_C_section       = 0;
num_Cminus_section  = 0;
num_Dplus_section   = 0;
num_D_section       = 0;
num_Dminus_section  = 0;
num_F_section       = 0;  
num_I_section       = 0;
num_W_section       = 0;
num_P_section       = 0;
num_NP_section      = 0;

num_A_group         = 0;
num_Aminus_group    = 0;
num_Bplus_group     = 0;
num_B_group         = 0;
num_Bminus_group    = 0;
num_Cplus_group     = 0;
num_C_group         = 0;
num_Cminus_group    = 0;
num_Dplus_group     = 0;
num_D_group         = 0;
num_Dminus_group    = 0;
num_F_group         = 0;
num_I_group         = 0;
num_W_group         = 0;
num_P_group         = 0;
num_NP_group        = 0;

#Browse files function which will be used when the user presses the browse files buttons to grab the file path
def browse_files():
    global directoryName, selectedFile, directory, directory_text
    file_types = [('Run Files', '*.RUN')]
    directory = filedialog.askopenfilename(filetypes=file_types)
    directory_text.set(directory)
    directoryName = (os.path.dirname(directory) + "/")
    data_path = directory
    selectedFile = os.path.basename(directory)

def getData(directoryName):

  #gets files from run file, puts in runfile dataframe
   Run_File = pd.read_csv(directoryName + selectedFile, skip_blank_lines=TRUE)
   Run_File.to_csv


   #make list of all group files names in runfile
   global grpList
   grpList = []
   grpList = Run_File.iloc[:, 0].values.tolist()

   #get size of group
   sizeOfGrp = len(grpList)

  #Construct Group_Files dataframe
   for i in range(len(grpList)):
  # tempDF = pd.read_csv(data_path + grpList[i], skip_blank_lines=TRUE) #temp dataframe that read in current group
     Group_Files = pd.DataFrame(grpList, columns=['Groups']);
   return Group_Files;

def run_commands():
    df = getData(directoryName)
    table = Table(frame, dataframe=df, showtoolbar=False, showstatusbar=False, editable=False)
    table.show()

data_path = os.path.dirname(os.path.realpath(__file__))

#creates a new column with the GPA based on letter grade
def calculate_gpa(df, grade_column='Letter_Grade'): 
    grade_point_map = {
        'A': 4.00,
        'A-': 3.67,
        'B+': 3.33,
        'B': 3.00,
        'B-': 2.67,
        'C+': 2.33,
        'C': 2.00,
        'C-': 1.67,
        'D+': 1.33,
        'D': 1.00,
        'D-': 0.67,
        'F': 0.00,
    }

    df['GPA'] = df[grade_column].map(grade_point_map)
    return df


def calculate_section_average(df, gpa_column='GPA'): 
  #Returns the average GPA of a section by 
  #averaging together all values in the GPA column
  #of dataframe
    return df[gpa_column].mean()


def calculate_group_average(Section_Files): 
#returns the average GPA from a grp file 

  gpa_group = 0.00; #GPA of group
  gpa_total = 0.00; #Total of all section gpas before divison


#For each section in Section_Files dataframe, calculate section GPA and add to GPA total
  for i in range(0, (Section_Files.shape[0])):
    Current_Section = pd.read_csv(directoryName + Section_Files.iloc[i, 0], header = 0, names=['Name', 'Student_ID', 'Letter_Grade'], skip_blank_lines=TRUE);
    gpa_section = 0.00;
    calculate_gpa(Current_Section);
    gpa_section = calculate_section_average(Current_Section);
    gpa_total += gpa_section;

  #Calculate GPA of group by dividing gpa_total by number of sections
  gpa_group = (gpa_total / (Section_Files.shape[0]));

  #Return group GPA
  return gpa_group;
def count_grades(df, grade_column='Letter_Grade'):

 #Void function that counts grades for a specified section and adds them to
 #to group and section total

 #References variables defined in for loop A
  global num_A_section
  global num_Aminus_section
  global num_Bplus_section 
  global num_B_section      
  global num_Bminus_section  
  global num_Cplus_section   
  global num_C_section       
  global num_Cminus_section  
  global num_Dplus_section   
  global num_D_section      
  global num_Dminus_section 
  global num_F_section       
  global num_I_section       
  global num_W_section       
  global num_P_section       
  global num_NP_section     

  #References variables defined in for loop B
  global num_A_group
  global num_Aminus_group
  global num_Bplus_group 
  global num_B_group      
  global num_Bminus_group  
  global num_Cplus_group   
  global num_C_group       
  global num_Cminus_group  
  global num_Dplus_group   
  global num_D_group      
  global num_Dminus_group 
  global num_F_group       
  global num_I_group       
  global num_W_group       
  global num_P_group       
  global num_NP_group     
  #For loop to iterate through each row of current section dataframe, retrieving each letter grade
  for i in range(0, len(df[grade_column])):

    #Retrieve grade from Current section dataframe at specified index
    grade = df[grade_column].iloc[i];


   #NOT RUNNING PYTHON 3.10, SWITCH STATEMENT MUST BE SERIES OF ELIF

   #Operates as a switch statement, throws error if no grade matches input
    if(grade== 'A'):
        num_A_section += 1;
        num_A_group += 1;
    elif(grade== 'A-'):
        num_Aminus_section += 1;
        num_Aminus_group += 1;
    elif(grade== 'B+'):
        num_Bplus_section += 1;
        num_Bplus_group += 1;
    elif(grade== 'B'):
        num_B_section += 1;
        num_B_group += 1;
    elif(grade== 'B-'):
        num_Bminus_section += 1;
        num_Bminus_group += 1;
    elif(grade== 'C+'):
        num_Cplus_section += 1;
        num_Cplus_group += 1;
    elif(grade== 'C'):
        num_C_section += 1;
        num_C_group += 1;
    elif(grade== 'C-'):
        num_Cminus_section += 1;
        num_Cminus_group += 1;
    elif(grade== 'D+'):
        num_Dplus_section += 1;
        num_Dplus_group += 1;
    elif(grade== 'D'):
        num_D_section += 1;
        num_D_group += 1;
    elif(grade== 'D-'):
        num_Dminus_section += 1;
        num_Dminus_group += 1;
    elif(grade== 'F'):
        num_F_section += 1;
        num_F_group += 1;
    elif(grade== 'I'):
        num_I_section += 1;
        num_I_group += 1;
    elif(grade== 'W'):
        num_W_section += 1;
        num_W_group += 1;
    elif(grade== 'NP'):
        num_NP_section += 1;
        num_NP_group += 1;
    elif(grade== 'P'):
        num_P_section += 1; 
        num_P_group += 1;
    else:
      #Error must be thrown describing an incorrect value in field, end program?
      print("error");

def generate_sect_avg_list(Section_Files):
  section_averages = []
  #Iterates through Section_Files df, gets GPA of each section, and appends it to a list of section_averages. 
  #Returns list of section averages
  for i in range(0, (Section_Files.shape[0])):
    Current_Section = pd.read_csv(directoryName + Section_Files.iloc[i, 0], header = 0, names=['Name', 'Student_ID', 'Letter_Grade'], skip_blank_lines=TRUE);
    gpa_section = 0.00;
    calculate_gpa(Current_Section);
    gpa_section = calculate_section_average(Current_Section);
    section_averages.append(gpa_section);
  return section_averages;

def z_test(section, Section_Files, gpa_group, stDev):

  #Perform z test on specific group
  z_score = (section - gpa_group) / (stDev / math.sqrt(Section_Files.shape[0]));

  #check for significance
  if z_score >= 2 or z_score <= -2:
      return 1;
  return 0; 

def z_compare(Section_Files, gpa_group): 
  #define temp num used for average & stdev calculation
  temp = 0;

  #define significance list
  sig_list = []
  section_averages = generate_sect_avg_list(Section_Files);

  #Calculate group standard deviation
  for i in range(0, Section_Files.shape[0]):
    temp = temp + ((section_averages[i]- gpa_group) ** 2);
    xyz = temp / Section_Files.shape[0];
    stDev = math.sqrt(abs(xyz))

    #Perform Z test
  for i in range(0, Section_Files.shape[0]):

    #determine significant by calling z_test
    significant = z_test(section_averages[i], Section_Files, gpa_group, stDev);

    #append significance value (1 or 0) to sig list
    sig_list.append(bool(significant));

    #construct significance dataframe and append to group dataframe
  sig_df = pd.DataFrame(sig_list, columns=['Significant']);
  Section_Files = pd.concat([Section_Files, sig_df], axis = 1);

    #Return updated Section_Files dataframe
  return Section_Files;   


#MAIN  Program
def main_program():

  #Input files & construct df
  global Group_Files
  Group_Files = getData(directoryName)

  ######### FOR LOOP A ###########################################################################
  #----Before Loop B execution----------------------------------------------------------------
  #0) Define current_group which holds the current group from the Group_Files dataframe
  #1) Define string name_group which holds the name of current group without extension
  #2) Define float gpa_group which holds the total GPA of current  group
  #3) Define ints that count total number of each grade (A-F) and (I, W, NP, P)
  #4) Define int that counts the total number of students in group
  #5) Define Section_Files dataframe that consists of all sections in the current group by reading contents of group file for current group
  #6) Define int that counts the number of sections in a group
  #7) Calculate the GPA of the group by calling calculate_group_average on Section_Files
  #8) Add 'Significance' column to Section_Files dataframe by calling z_compare. Determine significance of each section
  #----After Loop B execution-------------------------------------------------------------
  #9) Define contents of Group Output dataframe
  #10) Define Group Output Dataframe (using group_output_data)
  #11) Append Group_Output to list of output dataframes
  ###################################################################################################

  #Iterate through each group file in Group_Files dataframe
  for i in range(0, (Group_Files.shape[0])):

    #0) Define current_group which holds the current group from the Group_Files dataframe
    current_group = Group_Files.iloc[i, 0];

    #1) Define string name_group which holds the name of current group without extension
    tempTuple = os.path.splitext(current_group)
    name_group = tempTuple[0];

    #2) Define int gpa_group which holds the total GPA of current  group
    gpa_group           = 0; 

    #3) Define ints that count total number of each grade (A-F) and (I, W, NP, P)
    global num_A_group         
    global num_Aminus_group    
    global num_Bplus_group     
    global num_B_group         
    global num_Bminus_group    
    global num_Cplus_group     
    global num_C_group         
    global num_Cminus_group    
    global num_Dplus_group     
    global num_D_group         
    global num_Dminus_group    
    global  num_F_group         
    global num_I_group         
    global num_W_group         
    global num_P_group         
    global num_NP_group     
    global group_dfs
    global section_dfs 
    global grade_dfs 

    global Section_Output 

    Section_Output = pd.DataFrame()  

    num_A_group         = 0;
    num_Aminus_group    = 0;
    num_Bplus_group     = 0;
    num_B_group         = 0;
    num_Bminus_group    = 0;
    num_Cplus_group     = 0;
    num_C_group         = 0;
    num_Cminus_group    = 0;
    num_Dplus_group     = 0;
    num_D_group         = 0;
    num_Dminus_group    = 0;
    num_F_group         = 0;
    num_I_group         = 0;
    num_W_group         = 0;
    num_P_group         = 0;
    num_NP_group        = 0;

    #4) Define int that counts the total number of students in group 
    num_student_group   = 0;

    #define seclist
    secList = []



    #5) Define Section_Files dataframe by reading contents of group file for current group
    Section_Files = pd.read_csv(directoryName + current_group, skip_blank_lines=TRUE)


    #6) Define int that counts the number of sections in a group
    num_section = Section_Files.shape[0];
    #7) Calculate the GPA of the group by calling calculate_group_average on Section_Files
    gpa_group = calculate_group_average(Section_Files);

    #8) Add 'Significance' column to Section_Files dataframe by calling z_compare. Determine significance of each section
    Section_Files = z_compare(Section_Files, gpa_group);

    ######### FOR LOOP B #######################################
    #Purpose: The purpose of For-Loop B is to iterate through all sections in the Section_Files dataframe, gather necessary data, 
    # perform calculations and comparisons, and provide this data in an output dataframe
    #----------------------------------------------------------------------------------------------------------------
    #0) Retrieve current section from Section_Files dataframe
    #1) Define string name_section which holds the name of current group without extension
    #2) Retrieve section significance value from 'Significant' column of Section_Files dataframe
    #3) Define ints that count number of students in current section
    #4) Define float that holds GPA of the current section
    #5) Define ints that count number of each grade in current section
    #6) Define df 'Current_Section' which constructs a dataframe for the current section
    #7) Determine number of students in a section by counting rows in Current_Section dataframe
    #8) Call calculate_gpa for Current_Section
    #9) Call calculate_section_average on Current_Section to determine section GPA.
    #10) Call count_grades to determine number of each grade in current section. (automatically adds to group total in function)
    #11) Define contents of Section Output dataframe
    #12) Define Section Output Dataframe (using section_output_data) 
    #13) Append Section_Output to list of output dataframes
    #GPA_mean = []
    for i in range(0, (Section_Files.shape[0])):

      #0) Retrieve current section from Section_Files dataframe
      curr_section = (Section_Files.iloc[i, 0]);

      #1) Define string name_section which holds the name of current section without  SEC extension
      tempTuple = os.path.splitext(curr_section)
      name_section = tempTuple[0];

      #2) Retrieve section significance value for current section from 'Significant' column of Section_Files dataframe
      significance = Section_Files.iloc[i, 1];

      #3) Define int that count number of students in current section
      num_student_section = 0;

      #Define float that holds GPA of the current section
      gpa_section         = 0.00;

      #5) Define ints that count number of each grade in current section
      global num_A_section       
      global num_Aminus_section  
      global num_Bplus_section  
      global num_B_section       
      global num_Bminus_section  
      global num_Cplus_section   
      global num_C_section       
      global num_Cminus_section  
      global num_Dplus_section   
      global num_D_section       
      global num_Dminus_section  
      global num_F_section         
      global num_I_section       
      global num_W_section      
      global num_P_section       
      global num_NP_section   
      global grade_dfs   

      num_A_section       = 0;
      num_Aminus_section  = 0;
      num_Bplus_section   = 0;
      num_B_section       = 0;
      num_Bminus_section  = 0;
      num_Cplus_section   = 0;
      num_C_section       = 0;
      num_Cminus_section  = 0;
      num_Dplus_section   = 0;
      num_D_section       = 0;
      num_Dminus_section  = 0;
      num_F_section       = 0;  
      num_I_section       = 0;
      num_W_section       = 0;
      num_P_section       = 0;
      num_NP_section      = 0;


      #6) Define df 'Current_Section' which constructs a dataframe for the current section 
      Current_Section = pd.read_csv(directoryName + curr_section, header = 0, names=['Name', 'Student_ID', 'Letter_Grade'], skip_blank_lines=TRUE);

      #7) Determine number of students in a section by counting rows in Current_Section dataframe
      num_student_section = Current_Section.shape[0];
      num_student_group += num_student_section; #add to total students in group

      #8) Call calculate_gpa for Current_Section
      calculate_gpa(Current_Section);

      #9) Call calculate_section_average on Current_Section to determine section GPA.
      gpa_section = calculate_section_average(Current_Section);

      #10) Call count_grades to determine number of each grade in current section. (automatically adds to group total in function)
      count_grades(Current_Section);

      #11) Define contents of Section Output dataframe
      section_output_data = {
          'Group_Name'   :  [name_group],
          'Section_Name' : [name_section],
          '# Students' : [num_student_section],
          '# A' :   [num_A_section],
          '# A-' :   [num_Aminus_section],
          '# B+' :  [num_Bplus_section],
          '# B' :   [num_B_section],
          '# B-' :  [num_Bminus_section],
          '# C+' :  [num_Cplus_section],
          '# C' :   [num_C_section],
          '# C-' :  [num_Cminus_section],
          '# D+' :  [num_Dplus_section],
          '# D' :   [num_D_section],
          '# D-' :  [num_Dminus_section],
          '# F' :   [num_F_section],
          '# I' :   [num_I_section],
          '# W' :   [num_W_section],
          '# P' :   [num_P_section],
          '# NP' :  [num_NP_section],
          'GPA' :   [round(gpa_section, 3)],
          'Significant' : [significance]


      }

      sec_grade_data = [
        num_A_section,
        num_Aminus_section,
        num_Bplus_section,
        num_B_section,
        num_Bminus_section,
        num_Cplus_section,
        num_C_section,
        num_Cminus_section,
        num_Dplus_section,
        num_D_section,
        num_Dminus_section,
        num_F_section,
        num_I_section,
        num_W_section,
        num_P_section,
        num_NP_section,
      ]

      #append data to seclist
      secList.append(section_output_data)
      grade_dfs[name_section] = sec_grade_data;

  #9) Define contents of Group Output dataframe
    global group_output_data
    group_output_data = {
        'Group_Name' : [name_group],
        '# Sections'  : [num_section],
        '# Students' : [num_student_group],
        '# A' :   [num_A_group],
        '# A-' :   [num_Aminus_group],
        '# B+' :  [num_Bplus_group],
        '# B' :   [num_B_group],
        '# B-' :  [num_Bminus_group],
        '# C+' :  [num_Cplus_group],
        '# C' :   [num_C_group],
        '# C-' :  [num_Cminus_group],
        '# D+' :  [num_Dplus_group],
        '# D' :   [num_D_group],
        '# D-' :  [num_Dminus_group],
        '# F' :   [num_F_group],
        '# I' :   [num_I_group],
        '# W' :   [num_W_group],
        '# P' :   [num_P_group],
        '# NP' :  [num_NP_group],
        'GPA' :   [round(gpa_section, 3)],


      }

    #10) Define Group Output Dataframe (using group_output_data)


    group_grade_data = [
        num_A_group,
        num_Aminus_group,
        num_Bplus_group,
        num_B_group,
        num_Bminus_group,
        num_Cplus_group,
        num_C_group,
        num_Cminus_group,
        num_Dplus_group,
        num_D_group,
        num_Dminus_group,
        num_F_group,
        num_I_group,
        num_W_group,
        num_P_group,
        num_NP_group,
      ]
    grade_dfs[name_group] = group_grade_data;
    #create merged dataframe with all sections data
    Section_Output = pd.DataFrame(secList, columns=['Group_Name', 'Section_Name', '# Students', 'Significant',  'GPA', '# A', '# A-', '# B+', '# B', '# B-','# C+', '# C','# C-',
      '# D+','# D','# D-', '# F','# I','# W','# P' ,'# NP'])


    #13) Append Section_Output to dict of sec dfs


    section_dfs[name_group] = Section_Output;
    #Group_Output = pd.DataFrame(group_output_data)
    Group_Output = pd.DataFrame(group_output_data, columns=['Group_Name', '# Sections', '# Students', 'GPA', '# A', '# A-', '# B+', '# B', '# B-','# C+', '# C','# C-',
      '# D+','# D','# D-', '# F','# I','# W','# P' ,'# NP'])

    #11) Append Group_Output to list of output dataframes
    group_dfs[name_group] = Group_Output

  # get our time variable
  time = date_time()
  #set our file name output
  output_file_name = directoryName + "Output" + time + ".txt"

  #Write output to file
  with open(output_file_name, "a") as f:
    f.write(".GRP  files found in the .RUN file \n")
    f.write("\n")
  write_file(directoryName, group_dfs, time)

  with open(output_file_name, "a") as f:
    f.write(".SEC  files found in the .GRP files \n")
    f.write("\n")
  write_file(directoryName, section_dfs, time)

  with open(output_file_name, "a") as f:
    f.write("File Created on " + time + "\n")
  groupsFrame()
def end_program():
    window.quit()
    window.destroy()
    sys.exit()
#gui main 

#RemoveExtension functionunction removes the path of a file and returns just the file name 
def removeExtension(file_name):
    base_name, extension = os.path.splitext(file_name)
    return base_name


def updateTableValues():

   global groupTableDisplayed
   global groupTable
   global runTableDisplayed
   global frameindex
   global selectedGroup

   comboboxSelection = section_combobox.get()
   selectedGroup = removeExtension(comboboxSelection)
   if(selectedGroup != ""):
    if(frameindex != 4):
        guistack.append(frameindex)
    if(runTableDisplayed == True):
        groupListFrame()

    elif (groupTableDisplayed == True):
        sectionsFrame()

def updateComboBox():
  global section_combobox
  global section_list_combobox
  if(frameindex !=4):
    df = getData(directoryName)
    section_combobox['values'] = df.iloc[:, 0].tolist()
    new_values = df['Groups'].tolist() 

    section_combobox['values'] = []

    section_combobox['values'] = new_values
  if(frameindex == 4):
    df = section_dfs[selectedGroup]
    section_list_combobox['values'] = df.iloc[:, 0].tolist()
    new_values = df['Section_Name'].tolist()

    section_list_combobox['values'] = []
    section_list_combobox['values'] = new_values

def goBack():
  global frame
  frame.grid_forget()
  frameindex = guistack.pop()
  if(frameindex == 1):
    homeFrame();
  if(frameindex == 2):
    groupsFrame()
  if(frameindex == 3):
    groupListFrame();
  if(frameindex == 4):
    sectionsFrame()
  
#function that outputs the current date and time
def date_time():
  #uses datetime.now() to grab the current date and time
  current = datetime.now()
  str_current = str(current)
  #this is the date and time format that we set 
  str_current = current.strftime("%m-%d-%Y_%H-%M-%S") 
  #return the time
  return str_current


#This function creates a output file in the same directory of the .RUN file of the output
def write_file(path, data, time):
    #This function writes to the file
    with open(path + "Output" + time + ".txt", "a") as f:
        for key, value in data.items():
            f.write(f"{value} \n" )
            f.write("\n")

#The main section of the GUI
# The GUI uses multiple frames to accomplsh our programs goal
# To move frames we use pack_forget() or  grid_forget() to clear the frame

from PIL import Image, ImageTk

#Sets our frame as window
window = tk.Tk()
window.title("GPA Calculator")
window.state("zoomed")
frame = tk.Frame(window)
frameindex = 0;
window.protocol("WM_DELETE_WINDOW", end_program)

#These global variables are used for the pictures of the forward and back buttons

#This is the homeFrame function. 
#It sets up the first frame the user sees when they open the .exe file
def homeFrame():
  #defines global variables
  global section_combobox
  global directory_text
  global frame, guistack
  global frameindex
  global frame
  global sections

  #creates frame
  frameindex = 1;
  frame = tk.Frame(window)

  #clears current frame in case the user pressed the back button on the second frame
  frame.pack_forget()

  #sets up our grid
  frame.grid(row=0, column=0, padx=10, pady=10)

  #creates a label telling the user to select a runfile
  section_label = tk.Label(frame, text="Select a runfile:", font=("Garmond", 24))
  section_label.pack(side="top", pady=10)
  sections = []

  # Creates the browse button so the user can browse files
  browse_button = tk.Button(frame, width = 10 , height = 2, font=("Garmond", 24), text="Browse", command=browse_files, bg="white", fg='black')
  browse_button.pack(side="top", padx=10, pady=10)

  #creates the go button the user presses to enter the next frame
  go_button = tk.Button(frame, text="Go", command=main_program, font=("Garmond", 24),width=3, height=2)
  go_button.pack(side="top", padx=10, pady=10)
  go_button.pack(side="top")

  #creates a label that shows the user file path once they select a file
  directory_text = tk.StringVar()
  directory_label = tk.Label(frame, textvariable = directory_text)
  directory_label.pack(side="top", padx=50, pady=10)

  #packs and loads the frame
  frame.pack(side="top", fill="both", expand=True)

  guistack.append(frameindex)

#The next frame is called thegroupsFrame() This is the next frame that displays the grp files in the .RUN file
def groupsFrame():
  #define variables
  global table, runTableDisplayed, frame, frameindex, guistack, Group_Files, section_combobox, directory_text, selectedGroup

  #Set and clear frame
  frameindex = 2;
  frame.pack_forget()
  frame = tk.Frame(window)
  frame.grid(row=0, column=0, padx=10, pady=10)

  #forward button will bring the user to the next frame
  forward_button = tk.Button(frame, text="View Group", command=updateTableValues, bg="white", fg='black')
  forward_button.grid(row=0, column=4)

  #back button will bring the user to the last frame
  back_button = tk.Button(frame, text="Back", command=goBack, bg="white", fg='black')
  back_button.grid(row=0, column=3)

  directory_text = tk.StringVar()
  directory_label = tk.Label(frame, textvariable=directory_text)
  directory_label.grid(row=2, column=0, pady=10)

  #dropdown menue of all the groups
  section_combobox = ttk.Combobox(frame, values=sections)
  section_combobox.grid(row=2, column=1, padx=5)

  select_group_text = tk.Label(frame, text="Select a group:")
  select_group_text.grid(row=2, column=0, padx=(30,5))

  #creates the table in the code that displays the dataframe
  table = Table(frame, dataframe=Group_Files, showtoolbar=False, showstatusbar=False, editable=False)
  updateComboBox()
  table.show()
  runTableDisplayed = True

#Creates frame that displays all the groups 
def groupListFrame():
  #deines variables
  global frame
  global section_combobox
  global groupTableDisplayed,  runTableDisplayed, guistack
  global frameindex, selectedGroup

  frameindex = 3;

  frame.grid_forget()

  frame = tk.Frame(window)
  frame.grid(row=0, column=0, padx=10, pady=10)

  #creates froward and back buttons
  forward_button = tk.Button(frame, text="View Sections", command=updateTableValues, bg="white", fg='black')
  forward_button.grid(row=0, column=4)
  back_button = tk.Button(frame, text="Back", command=goBack, bg="white", fg='black')
  back_button.grid(row=0, column=3, padx=5)

  comboboxSelection = section_combobox.get()
  selectedGroup = removeExtension(comboboxSelection)

  #creates the button to display the graph
  graph_button = tk.Button(frame, text="View Graph", command=createHistogram, bg="white", fg='black')
  graph_button.grid(row=5, column=3, padx=5)

  #creates the table that displays the selected group
  newGroupDF = group_dfs[selectedGroup]
  table.grid_forget()
  runTableDisplayed = False
  groupTable = Table(frame, dataframe=newGroupDF, showtoolbar=False, showstatusbar=False,width=1000, editable=False)
  groupTable.show()

  #displays table
  groupTableDisplayed = True
  groupTable.redraw()
  section_combobox.grid_forget()

def createHistogram():
  if(frameindex == 4):
    createSectionHistogram()
    createGroupHistogram()
  else:
     createGroupHistogram()

#creates section histogram
def createSectionHistogram():
    #define variables
  global selectedSection
  global selectedGroup

  comboboxSelection = section_list_combobox.get() 
  selectedSection = removeExtension(comboboxSelection)
    
  #sets the x axis to the grades and y axis to the selected section
  x_axis = ['A', 'A-', 'B+', 'B', 'B-','C+', 'C','C-','D+','D','D-', 'F','I','W','P' ,'NP']
  y_axis = grade_dfs[selectedSection]

  #cosmetic stuff to make the graphs more readable
  colors = ['blue', 'royalblue']
  plt.grid(color='#95a5a6', linestyle='--', linewidth=2, axis='y', alpha=0.3)
  plt.figure(figsize=(6, 4))
  plt.bar(x_axis, y_axis, color=colors)
   
   # set our title and axis labels
  plt.title('Number of each grade in section: ' + selectedSection, weight='bold')
  plt.ylabel('Number of occurences', fontsize = 14)
  plt.xlabel('Grade Value', fontsize = 14)

  #add figure to the GUI
  canvas = FigureCanvasTkAgg(plt.gcf(), master=frame)
  canvas.draw()
  canvas.get_tk_widget().grid(row=6, column=0, columnspan=5, sticky='w')

#Creates the group histogram
def createGroupHistogram():
    comboboxSelection = section_combobox.get() 
    selectedGroup = removeExtension(comboboxSelection)

    #sets the x axis to the grades and y axis to the selected group
    x_axis = ['A', 'A-', 'B+', 'B', 'B-','C+', 'C','C-','D+','D','D-', 'F','I','W','P' ,'NP']
    y_axis = grade_dfs[selectedGroup]
    
    #cosmetic stuff to make the graphs more readable
    colors = ['darkred', 'firebrick']
    plt.grid(color='#95a5a6', linestyle='--', linewidth=2, axis='y', alpha=0.3)
    plt.figure(figsize=(6, 4))

    #set graph as a bar graph
    plt.bar(x_axis, y_axis, color=colors)
    
    # set our title and axis labels
    plt.title('Number of each grade in group: ' + selectedGroup, weight='bold')
    plt.ylabel('Number of occurences', fontsize = 14)
    plt.xlabel('Grade Value', fontsize = 14)

    #add figure to the GUI
    canvas = FigureCanvasTkAgg(plt.gcf(), master=frame)
    canvas.draw()
    canvas.get_tk_widget().grid(row=6, column=0, columnspan=5, sticky='e', padx=(0,120))


# creates the section frame
def sectionsFrame():

  #define variables  
  global section_combobox
  global frame, guistack
  global frameindex, selectedGroup
  global section_list_combobox
  global selectedSection

  #set frame
  frameindex = 4;
  frame.grid_forget()
  comboboxSelection = section_combobox.get()
  selectedGroup = removeExtension(comboboxSelection)
  frame = tk.Frame(window)
  frame.grid(row=0, column=0, padx=10, pady=10)

  #create back button
  back_button = tk.Button(frame, text="Back", command=goBack, bg="white", fg='black')
  back_button.grid(row=0, column=3)

  #create dropdown menue for the sections
  section_list_combobox = ttk.Combobox(frame, values=sections)
  section_list_combobox.grid(row=5, column=1, padx=5)
  updateComboBox()

  #put text in the combo box telling the user to select a file
  select_section_text = tk.Label(frame, text="Select a section:")
  select_section_text.grid(row=5, column=0, padx=(30, 5))

  #creates button that displays the graph
  graph_button = tk.Button(frame, text="View Graph", command=createHistogram, bg="white", fg='black')
  graph_button.grid(row=5, column=3, padx=5)

  #creates the table that displays the output section data
  newSectionDF = section_dfs[selectedGroup]
  sectionTable = Table(frame, dataframe=newSectionDF, showtoolbar=False, showstatusbar=False, width=1000, editable=False)
  sectionTable.show()
  sectionTable.redraw()


#creates the GUI
homeFrame()
window.mainloop()
