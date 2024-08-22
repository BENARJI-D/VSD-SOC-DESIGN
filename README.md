                                                        VLSI PHYSICAL DESIGN       
          Workshop contents
          
        1.Intro to Opensource EDA tool(OPENLANE) and PDK(skywater130nm)
        2.Floorplanning and Power planning
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

                                                            DAY-1 LAB
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
  
![image](https://github.com/user-attachments/assets/7841cf96-dd0e-475a-a154-4b80d0ea3c75)
![image](https://github.com/user-attachments/assets/85a50c62-00f6-4a58-8c57-e1352b432094)
![image](https://github.com/user-attachments/assets/81f8927c-0ab7-4d74-ac94-a630fb1cee56)
     FLOPS Ratio
Scereenshots of Synthesis report with NO.of Cells,No.FlipFlops

![image](https://github.com/user-attachments/assets/d3567bc0-817f-4aa3-a7b2-6e74dba13d2c)

![image](https://github.com/user-attachments/assets/2acc4db1-5dc8-4278-85e0-2687f4d81b1f)

Flop Ratio=(No.of D-FF/No.of cells)*100
 D-Flop Ratio  =1613/14876*100=10.8429%
 
                       DAY-2
                       
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
    Screen shot of Floorplan in Magic tool
    ![image](https://github.com/user-attachments/assets/e0eacc86-7407-4e78-9e6d-63b109647c87)
    Decap cells
    ![image](https://github.com/user-attachments/assets/8c6f9492-976d-4788-ae14-0a4e387a773f)
    Equidistant tap cells
    ![image](https://github.com/user-attachments/assets/cc4c03d6-2a55-4fb7-8482-18ca16fd6e12)
    Standard cells unplaced present at bootom left corner
    ![image](https://github.com/user-attachments/assets/9a3193e0-85f1-4a35-af0c-e433d1d14ace)
    #Command for placement run in openlane flow
    run_placement
    <img width="414" alt="image" src="https://github.com/user-attachments/assets/2ba246cb-3fbb-4b2f-abfb-15e6782d7341">
    
    <img width="292" alt="image" src="https://github.com/user-attachments/assets/c301d027-6152-4dfb-bd2f-359fbf94b1c7">

    <img width="383" alt="image" src="https://github.com/user-attachments/assets/c182640d-978d-4d28-89d2-222945e335dd">





 





 
 




