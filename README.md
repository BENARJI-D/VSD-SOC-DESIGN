                                                        VLSI PHYSICAL DESIGN       
          Workshop contents
          
        1.Intro to Opensource EDA tool(OPENLANE) and PDK(skywater130nm)
        2.GOOD VS BAD floorplan,Introduction to library cells
        3.Cell design using Magic and Ngspice
        4.Pre layout timing analysis,importance of good clock trees(min skew)
        5.Final steps for RTL2GDS using tritonRoute and openSTA

 DAY 1: Inception of open source EDA, openLANE, sky130 PDK

 
 How to talk to computers:
 
 ![image](https://github.com/user-attachments/assets/2b82a189-fb5a-4b7d-9b0a-49754360c6b0)
     
Physical design is focussing on the macro inside the processor and also block level design.
     
  ![image](https://github.com/user-attachments/assets/7070d7dd-3df0-4e35-ace3-21800b3bf415)
  
The above image shows a PCB on which different component placed.
             
 ![image](https://github.com/user-attachments/assets/50bf7477-91dd-47f6-b6d9-818d7998e4dc)
![image](https://github.com/user-attachments/assets/c8cc3ba9-8042-4cf5-8392-81d29d6290c1)

CORE: It is the section of the chip where the fundamental logic of the design is placed.

DIE: A die, which consists of core, is small semiconductor material specimen on which the fundamental circuit is fabricated.

IO PADS: Pads are normally distributed around the edge of the IC. The pad should be large enough to have input or output circuitry.  Here, the pad is built to a standard width and height. The pad has large VDD and ground lines. The pad includes large piece of metal.

IP: An IP (intellectual property) core is a block of logic or data that is used in making a field programmable gate array (FPGA) or application-specific integrated circuit (ASIC) for a product.

PDK: A Process Design Kit (PDK) is a library of basic photonic components generated by the foundry to give open access to their generic process for fabrication.

SIMPLIFIED RTL TO GDS FLOW

![WhatsApp Image 2024-08-20 at 10 52 11_f64999f6](https://github.com/user-attachments/assets/265f2f4e-d02b-4909-aa0f-98fed32dc057)

OPENLANE ASIC FLOW
             
Open LANE is an open-source EDA toolchain designed for digital ASIC design and optimization, it has open everything SOC’S,OPEN PDK’S,OPEN EDA,OPEN RTL. It integrates various tools and flows to streamline the design process from RTL to GDSII. It produce clean GDSII with no human intervention. 
             
![image](https://github.com/user-attachments/assets/1c508b8a-7404-417b-a23f-1e23cd4618ab)

                                                           
                                    DAY-1 -Inception of EDA,OPENLANE,SKY130 PDK
           
"Picorv32a" design synthesis using OPENLANE flow

#Change Directory to openlane directory

cd Desktop/work/tools/openlane_working_dir/openlane

#To invoke openlane flow use command docker

  docker

#setting openlane flow to be interactive mode

  ./flow.tcl -interactive

#input the openlane require package

  package require openlane 0.9

#Now prep the design for the openlane flow

  prep -design picorv32a

#run the synthesis using the command

  run_synthesis
  
  Screenshots of each running commands
  
![image](https://github.com/user-attachments/assets/7841cf96-dd0e-475a-a154-4b80d0ea3c75)
![image](https://github.com/user-attachments/assets/85a50c62-00f6-4a58-8c57-e1352b432094)
![image](https://github.com/user-attachments/assets/81f8927c-0ab7-4d74-ac94-a630fb1cee56)
     
       
FLOPS Ratio
     
Scereenshots of Synthesis report with NO.of Cells,No.FlipFlops

![image](https://github.com/user-attachments/assets/d3567bc0-817f-4aa3-a7b2-6e74dba13d2c)

![image](https://github.com/user-attachments/assets/2acc4db1-5dc8-4278-85e0-2687f4d81b1f)

Flop Ratio=(No.of D-FF/No.of cells)*100

 D-Flop Ratio  =1613/14876*100=10.8429%
 
 
DAY-2 -GOOD vs BAD floorplan,Intro to library cells
                       
i)FLOORPLAN run using OPENLANE flow
    
#To invoke openlane flow use command docker

  docker

#setting openlane flow to be interactive mode

  ./flow.tcl -interactive

#input the openlane require package

  package require openlane 0.9

#Now prep the design for the openlane flow

  prep -design picorv32a

#run the synthesis using the command

  run_synthesis
  
#run floorplan using this command

  run_floorplan

![image](https://github.com/user-attachments/assets/e551e518-a6a2-4cf0-9cc1-ac4fbc78175f)

 ii)Die area calculation for floorplan def
 
 Screen shot of Floorplan def
 
 ![image](https://github.com/user-attachments/assets/fb9e4218-7a9f-4057-84b8-31480a508de5)
  
Fom def

   1000 unit distance=1 micron
   
   Die width=660685/1000=660.685 microns
   
   Die height=671405/1000=671.405 microns
   
   Die area=660.685*671.405=443587.212 microns square
   
iii)Magic tool to visualize floorplan using floorplan def file

#Command to set the directory to run magic toolc

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

#Command for loading floorplan def in Magic tool

    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &
    
    Screen shot of Floorplan def in Magic tool
    
  ![image](https://github.com/user-attachments/assets/e0eacc86-7407-4e78-9e6d-63b109647c87)
    Decap cells
    ![image](https://github.com/user-attachments/assets/8c6f9492-976d-4788-ae14-0a4e387a773f)
    Equidistant tap cells
    ![image](https://github.com/user-attachments/assets/cc4c03d6-2a55-4fb7-8482-18ca16fd6e12)
    Standard cells unplaced present at bootom left corner
    ![image](https://github.com/user-attachments/assets/9a3193e0-85f1-4a35-af0c-e433d1d14ace)
   
    After floorplan step is completed,next step is placement
    
    It consists of 2 stages 
    
    1.Global placement 
    
    2.Deatailed placement
    
    #Command for placement run in openlane flow
    
    run_placement
    
   ![image](https://github.com/user-attachments/assets/d8acc91e-f91d-4315-9202-bb3aec0ca737)

   ![image](https://github.com/user-attachments/assets/682e47d4-4b29-464b-910c-de18e66671bb)

   
#Set directory path placement def file containing directory
    
     cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/
     
    #Command for loading placement def in Magic tool
    
    magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read 
     ../../tmp/merged.lef def read picorv32a.placement.def &

     Screenshot of floorplan in magic tool
     
  ![image](https://github.com/user-attachments/assets/41e84a87-a1f0-4749-be40-83c861d967b3)

  
DAY-3-Design library cell using magic and ngspice
                  
SPICEDECK creation for CMOS Inverter

A spicedeck contains netlist with connectivity information,inputs,outputs tap points.Nodes are required for defining a netlist

![image](https://github.com/user-attachments/assets/c7e7fb1a-4011-46b0-a3a4-eeab833247b1)
![image](https://github.com/user-attachments/assets/b47ab06d-ec33-414b-a3e5-1e9870875068)

Comparision of SPICE results for different PMOS widths,which causes output characteristics switching happens.

![image](https://github.com/user-attachments/assets/91d781c7-ff2e-49a3-a41f-f55f05d0cb50)


INVERTER CHARACTERISTICS

Input low voltage:The highest input voltage that is still interpreted as logic 0.

Input high voltage:The lowest input voltage that is recognized as logic 1.

Output Low Voltage (Vol): The voltage level at which the output changes from a high state to a low state.

Output High Voltage (Voh): The voltage level at which the output changes from a low state to a high state.

Noise margins:The voltage ranges that define the tolerance for noise. The low noise margin is the range between Vil and Vol, while the high noise margin is the range between Vih and Voh.

Fabrication process of a CMOS

Creating active region for Tansistors

![image](https://github.com/user-attachments/assets/19c4c940-9461-4084-98e3-a4e399c9eb9f)

N-well,P-well formation

![image](https://github.com/user-attachments/assets/ee820353-7cba-4da5-9a3f-4b17fe083af1)
![image](https://github.com/user-attachments/assets/ff86bba5-d531-4ad0-bf00-24b890a76d19)

Formation of Gate
![image](https://github.com/user-attachments/assets/6d26a5b0-dd36-48c6-a36d-7c1dcccd06bf)
![image](https://github.com/user-attachments/assets/a9f09607-e411-46b3-a5c8-86201426e74a)

Lightly doped drain formation
![image](https://github.com/user-attachments/assets/5bef5247-cf90-4d2e-a5b4-6afc75ccd55c)
![image](https://github.com/user-attachments/assets/bd9ec88d-5ba4-483e-82f7-b14fa658c796)
![image](https://github.com/user-attachments/assets/a0ec6b56-88a3-43f2-9b1a-fdd254aa75d8)

Source and Drain formation
![image](https://github.com/user-attachments/assets/17954aba-d122-4ee6-898d-b41d051d0257)
![image](https://github.com/user-attachments/assets/f695212e-229a-4907-9c88-373ef57a3789)

steps to form contacts and interconnects
![image](https://github.com/user-attachments/assets/2508d2cf-acc6-4630-b91f-c7a8ae219faf)
![image](https://github.com/user-attachments/assets/2e1095f1-09be-4e50-b043-25944bf56d5b)
![image](https://github.com/user-attachments/assets/d2b491c0-eb59-43dc-86ac-8b05b2995a3a)

Higher level metal formation
![image](https://github.com/user-attachments/assets/9636fc90-a9e4-4b88-8a60-36f5502c3b43)
![image](https://github.com/user-attachments/assets/79966fb0-02e9-4252-bb0f-463f1df77b8b)
![image](https://github.com/user-attachments/assets/6a091059-3fc7-49a5-9e16-c978af9fdcd1)



i)Cloning std cell design from github repository
  
      # Change directory to openlane
      
      cd Desktop/work/tools/openlane_working_dir/openlane
      
      #Clone reposirory with std cell design
      
      git clone https://github.com/nickson-jose/vsdstdcelldesign

     # open std cell repo directory
     
     cd vsdstdcelldesign

     # Copy magic tech file to the repo directory for easy access
     
     cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

    # Command to open custom inverter layout in magic
    
    magic -T sky130A.tech sky130_inv.mag &


![image](https://github.com/user-attachments/assets/b89fa43c-e5e7-4756-b5e2-dbd6174fe381)
![image](https://github.com/user-attachments/assets/be0e83fc-4990-4fda-96d9-810739ec1adc)
![image](https://github.com/user-attachments/assets/6c61b777-e790-4037-9b79-ae7f4815d718)
![image](https://github.com/user-attachments/assets/ff620971-265d-4c22-8f23-0baea1313376)
![image](https://github.com/user-attachments/assets/61a974cd-60e7-4122-a312-2a8f51aaa223)
![image](https://github.com/user-attachments/assets/ba57d33b-ef96-4586-b86c-805f66c663b7)

ii)Inverter spice extraction from magic

 #In tkcon window use the following commands 
 
   pwd
   
 #Extraction command to extract to .ext format
 
  extract all

 #enable the parasitic extraction before converting ext to spice
  
  ext2spice cthresh 0 rthresh 0

 #Convert ext to spice
 
  ext2spice

  ![WhatsApp Image 2024-08-04 at 12 54 59_485f60f9](https://github.com/user-attachments/assets/95dece16-439d-40e8-8a26-5d9ecfe13791)
![WhatsApp Image 2024-08-04 at 14 25 16_bc5e6a5c](https://github.com/user-attachments/assets/b5e2bba8-40d9-4702-bc84-6a03da4d85c3)

iii)ngspice simulation

1-Rise time:The time taken for the output waveform to transition from 20% to 80% of its maximum value.

2-Fall time:The time taken for the output waveform to transition from 80% to 20% of its maximum value.

3-Cell Rise delay:The time taken for a 50% transition at the output (0 to 1) corresponding to a 50% transition at the input (1 to 0).

4-Cell fall delay:The time taken for a 50% transition at the output (1 to 0) corresponding to a 50% transition at the input (0 to 1).
    
#Command for loading spice file in ngspice simulation

ngspice sky130_inv.spice

#Spice file loaded,Now plot the graph uning the command

plot y vs time a

![image](https://github.com/user-attachments/assets/7e046260-9188-41ed-8341-95651e68c302)
![image](https://github.com/user-attachments/assets/caddad6b-52bf-4520-a79c-32a82a928455)
![image](https://github.com/user-attachments/assets/4fc3fb83-5702-4f91-aa22-1db5f7bd8d6b)
![image](https://github.com/user-attachments/assets/c9e83dd6-4064-4720-b931-8eeeaf35c6c8)
![image](https://github.com/user-attachments/assets/31d2c887-671a-495a-939a-83e46bed4bf7)
![image](https://github.com/user-attachments/assets/706cc34f-ddeb-42c5-b407-e3ab54edfdc9)

50% of 3.3v=1.65 v,input and output waveforms need to measure time at 1.65v for calculating rise and fall delays.

Rise cell delay=148ps

Fall cell delay=71ps

iv)Sky 130 PDK intro,Finding and fixing problems for DRC

#Change the directory to home directory

cd

#Command for downloading lab files

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

#command for extraction of lab files

tar xfz drc_tests.tgz

#Change directory into the lab files directory

cd drc_tests

#List all files present in the current directory

ls -ltr

#To view .magicrc file

gvim .magicrc

#Command to open magic tool

magic -d XR &

 Screenshots of DRC rules violations and corrections for no DRC violations

![image](https://github.com/user-attachments/assets/cf328f28-369b-4627-ac40-0866c731d76c)
![image](https://github.com/user-attachments/assets/37343b16-5a1c-44aa-8cc3-dee8d31c503d)
![image](https://github.com/user-attachments/assets/acc6b6c3-a5f9-4cf4-8154-cdd8f2a7164e)
![image](https://github.com/user-attachments/assets/4099ab3e-be1a-4f8f-934e-cb75bb52f444)
![image](https://github.com/user-attachments/assets/dcf55f60-8fbf-462a-84f8-67d95a3e41b2)
![image](https://github.com/user-attachments/assets/2ed57216-3a9f-4c24-b2c0-d801678f3c36)
![image](https://github.com/user-attachments/assets/052a1a13-e3ba-4c88-be63-069a128eef87)
![image](https://github.com/user-attachments/assets/c38fa5d0-1ae1-470c-bb3b-5cc7a0d0a45d)
![image](https://github.com/user-attachments/assets/eff0a139-477d-44a9-b3be-620ee2477b9a)
![image](https://github.com/user-attachments/assets/bef26b99-0097-41b6-9892-9bf3ae617a04)
![image](https://github.com/user-attachments/assets/847f67b5-32f7-4396-b3f6-e2d4c37c6c53)
![image](https://github.com/user-attachments/assets/5e1235ea-b96e-482e-b4c0-a4f3564a561d)

DAY-4 -Pre layout timing analysis and importance of Good clock tree


i)Delay tables,Timing analysis and CTS

Delay tables
        
At each level,Each node dricing same amound of load otherwise skew will be introduced into the network.
Identical buffers need to be used at same level.output transition of a cell is the function of input transition+output capacitace.

Timing modelling using delay tables
  
Converting grid information like rows and columns into track information is important.when designing standard cells,it is important to ensure that input and output ports aligned with intersections of horizontal and vertical tracks.

Standard cells width should be odd multiples of horizontal track pitch,height should be odd multiples of vertical track pitch.LEF file provides necessary information for the PNR flow process.tracks.info file contains horizontal and vertical tracks metal layer information.I t contains pitch,spacing data which are used for routing stage.
     
![image](https://github.com/user-attachments/assets/b287ba17-369f-4de3-9ff8-f4801318c423)
![image](https://github.com/user-attachments/assets/b4b218c3-762c-4afc-ba16-e50c8298848e)
![image](https://github.com/user-attachments/assets/520add47-99bf-4b44-b062-a422866496e7)
![image](https://github.com/user-attachments/assets/555e4d72-235d-475a-8161-253e6850ead4)
![image](https://github.com/user-attachments/assets/b5f9327e-27c7-4e7e-8e2a-ae5a5b834def)
![image](https://github.com/user-attachments/assets/fa68ba9e-6a36-4f5c-8552-6131ce662d4d)
![image](https://github.com/user-attachments/assets/2c056fef-09bc-47c7-a221-4203ffab8c80)
![image](https://github.com/user-attachments/assets/4114c5b9-9290-4c3c-8cf3-f0ab2ed8faad)
![image](https://github.com/user-attachments/assets/31bf6c81-3559-4700-adf6-e92e56e60536)

i)Conditions for to inclde our custom design in picorv32a design

1-Input&output ports should be lie on the intersection of horizontal and vertical tracks
  
2-Height of standard cell is even multiples of vertical track pitch.
  
3-Width of standard cell is odd multiples of horizontal track pitch.

  #change working directory to vsdstdcelldesign direcory
  
  cd Desktop/work/tools/openlane_working_dir/

  #command to open inverter layout in magic
  
  magic-T sky130A.tech sky130_inv.mag &

  Screenshots of tracks.info file opening,contents of file
  
  ![image](https://github.com/user-attachments/assets/8ba25e5d-f9e7-498e-bddd-2a5bf3fd2d7e)

  ![image](https://github.com/user-attachments/assets/1de06f7b-269d-4d99-a8fa-9a8bcb344551)

#command for setting grid values based on tracks.info file

grid 0.46um 0.34um 0.23m 0.17um

![image](https://github.com/user-attachments/assets/30a0ff81-3e75-4d08-a76a-06a4ff328e24)
![image](https://github.com/user-attachments/assets/dbca9e64-6808-40fd-881e-2a83ae34a242)
![image](https://github.com/user-attachments/assets/f503ad17-6dfc-4fcc-897a-3865b27557cd)
![image](https://github.com/user-attachments/assets/e7f34b54-6563-48cd-9091-d1914fabc232)
![image](https://github.com/user-attachments/assets/bd98989c-49d6-4ff9-b75b-29a5c77e01fe)

Copy new lef and library files to src directory

![image](https://github.com/user-attachments/assets/41624bcb-d723-4ea2-9881-77aab35bc388)


 ii) Edit config.tcl for to change lib file and added extra lef in openlane flow
 
  ![image](https://github.com/user-attachments/assets/a122a4ef-cc52-4ae0-94e6-8d0681b273a4)
  
  iii)Commands to run synthesis in openlane flow with new inverter cell
  
  #To invoke openlane flow use command docker

  docker

#setting openlane flow to be interactive mode

  ./flow.tcl -interactive

#input the openlane require package

  package require openlane 0.9

#Now prep the design for the openlane flow

  prep -design picorv32a -tag 31-07_05-36 -overwrite

#Commands for including newly lef to the openlane flow

set lefs [glob $::env(DESIGN_DIR)/src/*.lef

add_lefs -src $lefs

#Command for running synthesis 

run_synthesis

![image](https://github.com/user-attachments/assets/b8836729-9d58-4d47-805f-aa40e7cd508e)
![image](https://github.com/user-attachments/assets/95288fa8-6f9e-41f8-8242-6f9d2cbb0a4b)
![image](https://github.com/user-attachments/assets/898be5a6-bcee-4850-9d2f-fe76d97e31ed)

iii)By modifying design parameters we can reduce the new violations into the design

![image](https://github.com/user-attachments/assets/4556a3d8-7397-4a06-ba48-6881ce854f38)
![image](https://github.com/user-attachments/assets/99dd5d64-a85b-49c9-8278-a0fdeaa9e928)

#To invoke openlane flow use command docker

  docker

#setting openlane flow to be interactive mode

  ./flow.tcl -interactive
  
#Now prep design for update variables

prep -design picorv32a -tag 31-07_05-36 -overwrite

#Commands for include newlef to openlane 

set lefs [glob $::env(DESIGN_DIR)/src/*.lef

add_lefs -src $lefs

echo $::env(SYNTH_STRATEGY)

#Command for setting SYNTH_STRATEGY

set ::env(SYNTH_STRATEGY) "DELAY 3"

#Command for displaying SYNTH_BUFFERING

echo $::env(SYNTH_BUFFERING)

#Command for display value of variable SYNTH_SIZING

echo $::env(SYNTH_SIZING)

#Command for set new value for SYNTH_SIZING

set ::env(SYNTH_SIZING) 1

#Command for display current value of SYNTH_DRIVING_CELL

echo $::env(SYNTH_DRIVING_CELL)

#Command to run synthesis

run_synthesis

Screenshot of merged.lef in tmp directory

![image](https://github.com/user-attachments/assets/d98a44de-1a03-4617-8b05-78d31e5a2d77)
![image](https://github.com/user-attachments/assets/49da2720-dc6c-4f2c-a885-9f9c4f04ebed)
![image](https://github.com/user-attachments/assets/0649dab7-9e5c-44bd-a187-28429b0b1cd6)
![image](https://github.com/user-attachments/assets/01dbcdff-68da-4df1-8e45-bb55a171d41d)
![image](https://github.com/user-attachments/assets/3b69d0f0-474c-4955-9313-69ff01889542)

iv)Now run floorpland,placement and check whether the custom cell is present in the PnR flow

#Commands used for replacement"run_floorplan" command

init_floorplan

place_io

tap_decap_or

#Command for placement run

run_placement

![image](https://github.com/user-attachments/assets/43756159-0d38-44ac-b51f-e00ca21a5aa7)
![image](https://github.com/user-attachments/assets/7fe1e442-df72-469f-bd29-e0135c6555e5)
![image](https://github.com/user-attachments/assets/4c198593-6080-43e8-a8e1-c965df4dc6c6)
![image](https://github.com/user-attachments/assets/83f7bd9d-90a1-4efb-9ff8-466600343212)

Commands to load placement def in magic

![image](https://github.com/user-attachments/assets/f0445c64-394a-4b61-8e39-0cc6a824a2c6)
![image](https://github.com/user-attachments/assets/cfd59d39-2b89-47c5-9186-8e0ef97eb5dd)
![image](https://github.com/user-attachments/assets/b45948c0-aa3b-490c-99b5-a6dedebfac3f)

v)Post_synthesis timing analysis with openSTA tool

Present wns,tns are 0.

For static timing analysis, in openlane directory Created pre_sta.conf file
     
   ![image](https://github.com/user-attachments/assets/7b06975a-03f0-40c3-b152-511ca4683a73)
   
   Created my_bse.sdc file in src directory based on base.sdc file in openlane/scripts directory.
   
   ![image](https://github.com/user-attachments/assets/cfdbd871-4b4b-4975-a6d6-dbe52e985f8d)

 #Change directory to openlane
  
cd Desktop/work/tools/openlane_working_dir/openlane

#Command for invoking OpenSTA tool 

sta pre_sta.conf 

![image](https://github.com/user-attachments/assets/e6b9c9a0-2832-436f-9c0a-e3293c33a21e)
![image](https://github.com/user-attachments/assets/ee9ee1be-a272-41cb-b3fc-438c6a665b3e)
![image](https://github.com/user-attachments/assets/b21ea722-9ff4-4ca4-966c-7fa8ea1153a9)
![image](https://github.com/user-attachments/assets/aa02a71c-1765-4e02-bae1-7b8783414663)
![image](https://github.com/user-attachments/assets/19f3e7a9-d81a-40c0-be78-e67dbbf8b06f)
![image](https://github.com/user-attachments/assets/0988b0e4-cf3e-46f4-8eeb-8bed793c408b)


Due to more fanout value causing more delay,here we reduce the max fanout by using the following commands
    
vi)ECO timing fixing for clear all violations

#Report for particular connections for a net

report_net -connections _netnumber_

#Command for Replacing a particular cell

replace_cell _driverpin number_ sky130_fd_sc_hd__gate name with size

#Timing report check

report_checks -fields {net cap slew input_pins} -digits 4

  ![image](https://github.com/user-attachments/assets/bce04dc6-968c-47ef-97be-3ada30768a25)
  ![image](https://github.com/user-attachments/assets/37e51ec3-f9b2-4cd2-918b-995566df8ba6)
![image](https://github.com/user-attachments/assets/d97656bd-21f9-4c06-a045-31687625eeea)
![image](https://github.com/user-attachments/assets/3d89b434-67a0-4a31-a099-683463c6665b)
![image](https://github.com/user-attachments/assets/a8729cb9-6e11-4834-9438-6593a7c9ba49)
![image](https://github.com/user-attachments/assets/fde43744-7223-4e13-afc0-2d70d8fe6193)
 
Eco fix started when wns is 23.89 now it comes down to 22.823 by replacing some of the driver cells by upsizing based on the load connected to that particular net.
       
vii)replace old netlist with new netlist and do the PnR flow

First we need to copy the old netlist.To replace old netlist with new netlist to PnR flow,use write_verilog command

![image](https://github.com/user-attachments/assets/003ab086-d012-4661-bfb3-0115e9e5bb0b)

      
#Command for replacing old netlist

write_verilog /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-07_05-36/results/synthesis/picorv32a.synthesis.v

![image](https://github.com/user-attachments/assets/45b6d8a0-37b1-4345-a585-b959d1addec9)

It is confirmed that the old netlist is replaced by the updated netlist based on the _13161_ cell updation.

    #Command for running cts
    run_cts

![image](https://github.com/user-attachments/assets/73a25cf3-75ca-4e5b-b2e6-d9fb9ab36203)

viii)Post CTS timing analysis using OpenRoad

Screenshots of timing reports

![image](https://github.com/user-attachments/assets/11287fa4-a276-4fdf-a4a7-a6560f4303df)
![image](https://github.com/user-attachments/assets/a431d464-60a2-4d51-88ba-282cf3383494)
![image](https://github.com/user-attachments/assets/82f2adbe-b291-4e09-a4fe-eb98a451d941)
![image](https://github.com/user-attachments/assets/0c459a73-7a7f-4306-8036-91510ff923be)

           DAY-5 RTL2GDS using TritonRoute&OpenSTA

i)Cts step is complated,next need to create power distribution network,command for PD network

  gen_pdn
  
![image](https://github.com/user-attachments/assets/4f27b955-b5c9-4245-82ac-6c6e2ad3aa15)
![image](https://github.com/user-attachments/assets/a231c36a-4cbf-4c52-903f-e516eb283f03)

#Change directory to PD N/W def

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-07_05-36/tmp/floorplan/

#Command to view PDN def in magic tool

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &

![image](https://github.com/user-attachments/assets/7de724d8-7a5e-4a0f-b022-efae752d1989)



ii)Now do detailed routing using commands 

#Checking CURRENT_DEF
   
echo $::env(CURRENT_DEF)

#Check value for ROUTING_STRATEGY

echo $::env(ROUTING_STRATEGY)

#Command for detailed route 

run_routing

Screenshots of routing stage

![image](https://github.com/user-attachments/assets/4158b6b2-f0c6-4629-904b-115c99eb75e7)
![image](https://github.com/user-attachments/assets/decc4c08-f21f-4039-b4a6-862745b6da9e)

#Change directory to routed def directory

cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-07_05-36/results/routing/

#Command to check routed def in magic tool

magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.def &

![image](https://github.com/user-attachments/assets/2cd8a14b-3398-48a1-8732-a14e040fe39b)
![image](https://github.com/user-attachments/assets/944e84d9-9ed8-45b2-b432-dcd0d5941528)
![image](https://github.com/user-attachments/assets/1cb1bfad-4ebd-4b15-9b1b-57b9b21b9c31)
![image](https://github.com/user-attachments/assets/31da291f-08fd-4502-a46c-da47fac8a3b5)

Screenshot of fastroure guide

![image](https://github.com/user-attachments/assets/53f614e2-7450-4810-a785-d99e415a353f)

iii)Parasitic extraction using SPEF extractor

#Change directory

cd Desktop/work/tools/SPEF_EXTRACTOR

#Command extract spef

python3 main.py 
/home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-07_05-36/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/31-07_05-36/results/routing/picorv32a.def

iv)Post-Route timing analysis using extracted parasitic in OPENROAD

![image](https://github.com/user-attachments/assets/8dbcb2cf-e9f7-4e1a-8afe-cd075c4c3b97)
![image](https://github.com/user-attachments/assets/54de82fa-4eb3-4040-8974-1676e23a7f12)
![image](https://github.com/user-attachments/assets/833c79fb-69ab-4522-8291-2cb8334e984b)
![image](https://github.com/user-attachments/assets/62e64905-3479-4fca-a3d7-192a719b3e87)



















  








    
    
 





      
      

  











  






















 



  
  










  



























  


  
  




    
     
    
    


    


    

    

    


    
    






 





 
 




