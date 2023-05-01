Download Link: https://assignmentchef.com/product/solved-blg222-final-exam-software-based-microprogrammed-control-unit
<br>
Design a <strong>software-based (microprogrammed) control unit</strong> for the following architecture. Use the structure shown in Figure 1 which is a slightly modified version of <strong>Project2.</strong>

You have to <strong>design and decide</strong> the size of the control memory and microinstruction format in order to control the simple computer. In addition, you might need to change the mapping algorithm as well.

<table width="487">

 <tbody>

  <tr>

   <td width="181">


    <table width="151">

     <tbody>

      <tr>

       <td width="48">MuxASel</td>

       <td width="103">MuxAOut</td>

      </tr>

      <tr>

       <td width="48">00011011</td>

       <td width="103">IROut (0-7)Memory OutputAddress Register OutCOutALU</td>

      </tr>

     </tbody>

    </table></td>

   <td width="168">


    <table width="112">

     <tbody>

      <tr>

       <td width="48">MuxBSel</td>

       <td width="64">MuxBOut</td>

      </tr>

      <tr>

       <td width="48">00011011</td>

       <td width="64">ɸIROut (0-7)Memory OutputOutALU</td>

      </tr>

     </tbody>

    </table></td>

   <td width="139">


    <table width="112">

     <tbody>

      <tr>

       <td width="48">MuxCSel</td>

       <td width="64">MuxCOut</td>

      </tr>

      <tr>

       <td width="48">01</td>

       <td width="64">MuxAOutOutA</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

 </tbody>

</table>

<em>Figure 1: Slightly Modified Version of Project 2 (i.e., here MUXC takes input from Address </em>

<em>Register File instead of MUXA) </em>

<em> </em>

<h1>INSTRUCTION FORMAT</h1>

There are two types of instructions as described below.

<strong>(1)</strong> Instructions with address reference has the format shown in Figure 2:

<ul>

 <li>The OPCODE is a 5-bit field (See Table 1 for the definition).</li>

 <li>The REGSEL is a 2-bit field (See left side of Table 2 for the definition).</li>

 <li>The ADDRESSING MODE is a 1-bit field (See Table 3 for the definition).</li>

 <li>The ADDRESS is 8 bits</li>

</ul>

<table width="602">

 <tbody>

  <tr>

   <td width="156">OPCODE</td>

   <td width="155">REGSEL</td>

   <td width="156">ADDRESSING MODE</td>

   <td width="135">ADDRESS</td>

  </tr>

 </tbody>

</table>

<h2>Figure 2: Instructions with an address reference</h2>

<strong>(2)</strong> Instructions without address reference has the format shown in Figure 3:

<ul>

 <li>The OPCODE is a 5-bit field (See Table 1 for the definition).</li>

 <li>DESTREG is a 3-bit field which specifies the destination register (See right side of Table 2 for the definition).</li>

 <li>SRCREG1 is a 3-bit field which specifies the first source register (See right side of Table 2 for the definition).</li>

 <li>SRCREG2 is a 3-bit field which specifies the second source register (See right side of Table 2 for the definition).</li>

 <li>The least significant two bits are unused and have the value 00.</li>

</ul>

<strong>At most one </strong>register from the address register file (AR/SP/PC) can be used on the <strong>right hand side</strong> of the instructions without address reference. In addition, if one of AR/SP/PC is used on the right hand side, it must be the A input of ALU (i.e., must be supplied by means of MUXC).

<table width="570">

 <tbody>

  <tr>

   <td width="148">OPCODE</td>

   <td width="147">DESTREG</td>

   <td width="147">SRCREG1</td>

   <td width="127">SRCREG2</td>

  </tr>

 </tbody>

</table>

00

<em>Figure 3: Instructions without an address reference</em>

Table 1: OPCODE field and  SYMBols for opertions and their descriptions

<em> </em>Table 2:REGSEL (Left) and DESTREG/SRCREG1/SRCREG2 (Right) select the register of interest for a particular instruction

Table 3: Addressing modes

EXAMPLE

The code given below adds data that are stored at M[A0]+M[A1]+M[A2]+M[A3]+M[A4] and stores the total at M[A5]. It is written as a loop that iterates 5 times.

You have to determine the binary code, write it into memory, and execute all these instructions.

ORG  0x20                                  # Write the program starting from the address 0x20

LD R0 IM 0x05                 #  R0 is used for iteration number

LD R1 IM 0x00                #  R1 is used to store total

LD R2 IM 0xA0

MOV AR R2                     # AR is used to track data adrress: starts from 0xA0

LABEL:   LD R2 D                            # R2 &lt;- M[AR] (AR = 0xA0 to 0xA4)

INC AR AR                      # AR &lt;- AR + 1 (Next Data)

<table width="572">

 <tbody>

  <tr>

   <td width="189">                ADD R1 R1 R2</td>

   <td width="47"> </td>

   <td width="336"># R1 &lt;- R1 + R2 (Total = Total + M[AR])</td>

  </tr>

  <tr>

   <td width="189">                DEC R0 R0</td>

   <td width="47"> </td>

   <td width="336"># R0 &lt;- R0 – 1 (Decrement Iteration Counter)</td>

  </tr>

  <tr>

   <td width="189">                BNE IM LABEL</td>

   <td width="47"> </td>

   <td width="336"># Go back to LABEL if Z=0 (Itertaion Counter &gt; 0)</td>

  </tr>

  <tr>

   <td width="189">                ST  R1 D</td>

   <td width="47"> </td>

   <td width="336"># M[AR] &lt;- R1 (Store Total at 0xA5)</td>

  </tr>

 </tbody>

</table>

<strong> </strong>