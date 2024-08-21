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
             
![image](https://github.com/user-attachments/assets/d0c065a2-581a-41d3-b3f9-207925c642
