## Intro

Code is running on Processing 3, with controlP5 graphical library. Pictures in the RMP folder are needed for background and buttons.

![RMP](/RMP/Fond.png)

## Processing code

```Java

import controlP5.*;

PImage bg;
PImage VHF1;
PImage VHF2;
PImage VHF3;
PImage HF1;
PImage HF2;
PImage AM;
PImage NAV;
PImage VOR;
PImage ILS;
PImage MLS;
PImage ADF;
PImage BFO;
PImage CHANGE;

ControlP5 cp5;
Button vhf1;
Button vhf2;
Button vhf3;
Button hf1;
Button hf2;
Button am;
Button nav;
Button vor;
Button ils;
Button mls;
Button adf;
Button bfo;
Button change;
Button ON;

Button plus1,moins1;
Button plus2,moins2;

Boolean[] mode = new Boolean [12];
//vhf1B,vhf2B,vhf3B,hf1B,hf2B,amB,navB,vorB,ilsB,mlsB,adfB,bfoB;
Boolean sel=false,on=true;

float active,standby;
//VHF = 118/136.975
//HF = 3/30
float vhf1AF=118.000,vhf1SF=119.000;
float vhf2AF=134.000,vhf2SF=125.000;
float vhf3AF=130.000,vhf3SF=135.000;
float hf1AF=3.000,hf1SF=4.000;
float hf2AF=30.000,hf2SF=29.000;
float amAF,amSF;


void setup() 
{
  size(873, 544);
  
  mode[0] = true;
  
  for(int i=1;i<12;i++)
  {
    mode[i] = false;
  }
  
  bg = loadImage("Fond.png");
  VHF1 = loadImage("VHF1.png");
  VHF2 = loadImage("VHF2.png");
  VHF3 = loadImage("VHF3.png");
  HF1 = loadImage("HF1.png");
  HF2 = loadImage("HF2.png");
  AM = loadImage("AM.png");
  NAV = loadImage("NAV.png");
  VOR = loadImage("VOR.png");
  ILS = loadImage("ILS.png");
  MLS = loadImage("MLS.png");
  ADF = loadImage("ADF.png");
  BFO = loadImage("BFO.png");
  CHANGE = loadImage("change.png");

  cp5 = new ControlP5(this);
  
  vhf1=cp5.addButton("VHF1")
    .setPosition(62, 184)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(VHF1);
    
   vhf2=cp5.addButton("VHF2")
    .setPosition(178, 186)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(VHF2);
    
   vhf2=cp5.addButton("VHF3")
    .setPosition(294, 186)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(VHF3);
    
   hf1=cp5.addButton("HF1")
    .setPosition(62, 286)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(HF1);
    
   hf2=cp5.addButton("HF2")
    .setPosition(294, 285)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(HF2);
    
   am=cp5.addButton("AM")
    .setPosition(418, 285)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(AM);
    
   nav=cp5.addButton("NAV")
    .setPosition(95, 428)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(NAV);
    
   vor=cp5.addButton("VOR")
    .setPosition(208, 429)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(VOR);
    
   ils=cp5.addButton("ILS")
    .setPosition(317, 429)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(ILS);
    
   mls=cp5.addButton("MLS")
    .setPosition(426, 429)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(MLS);
    
   adf=cp5.addButton("ADF")
    .setPosition(536, 429)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(ADF);
    
   bfo=cp5.addButton("BFO")
    .setPosition(646, 429)
    .setSize(83, 55)
    .setLabelVisible(false)
    .setImage(BFO);
   
   change=cp5.addButton("CHANGE")
    .setPosition(390, 76)
    .setSize(91, 69)
    .setLabelVisible(false)
    .setImage(CHANGE);
    
   plus1=cp5.addButton("PLUS1")
    .setPosition(686,270)
    .setSize(20,20);
    
   moins1=cp5.addButton("MOINS1")
    .setPosition(535,270)
    .setSize(20,20);
    
   plus2=cp5.addButton("PLUS2")
    .setPosition(646,270)
    .setSize(20,20);
    
   moins2=cp5.addButton("MOINS2")
    .setPosition(575,270)
    .setSize(20,20);
    
   ON=cp5.addButton("ON")
    .setPosition(758,400)
    .setSize(20,20);
}

// -------------- Draw -------------------------

void draw()
{
  background(bg); 

  freqUpdate();
  lightUpdate();
                    
}

// --------------- Light -----------------------

public void lightUpdate()
{
  if(mode[0])
  {
    noStroke();
    fill(0,255,0);
    circle(47,212,18);
  }
  else if(mode[1])
  {
    noStroke();
    fill(0,255,0);
    circle(164,213,18);
  }
  else if(mode[2])
  {
    noStroke();
    fill(0,255,0);
    circle(279,212,18);
  }
  else if(mode[3])
  {
    noStroke();
    fill(0,255,0);
    circle(47,310,18);
  }
  else if(mode[4])
  {
    noStroke();
    fill(0,255,0);
    circle(277,310,18);
  }
  else if(mode[5])
  {
    noStroke();
    fill(0,255,0);
    circle(401,311,18); 
  }
  else if(mode[6])
  {
    noStroke();
    fill(0,255,0);
    circle(131,416,18); 
    
    if(mode[7])
    {
      noStroke();
      fill(0,255,0);
      circle(193,455,18); 
    }
    else if(mode[8])
    {
      noStroke();
      fill(0,255,0);
      circle(301,455,18); 
    }
    else if(mode[9])
    {
      noStroke();
      fill(0,255,0);
      circle(411,455,18); 
    }
    else if(mode[10])
    {
      noStroke();
      fill(0,255,0);
      circle(520,455,18); 
    } 
    else if(mode[11])
    {
      noStroke();
      fill(0,255,0);
      circle(631,456,18); 
    }
  }
  
  if(!mode[0])
  {
      noStroke();
      fill(255,145,0);
      circle(224,329,18); 
  }
    
}
// --------------- Frequency -------------------
public void freqUpdate()
{
  if(mode[0])
  {
    active = vhf1AF;
    standby = vhf1SF;
  }
  else if(mode[1])
  {
    active = vhf2AF;
    standby = vhf2SF;
  }
  else if(mode[2])
  {
    active = vhf3AF;
    standby = vhf3SF;
  }
  else if(mode[3])
  {
    active = hf1AF;
    standby = hf1SF;
  }
  else if(mode[4])
  {
    active = hf2AF;
    standby = hf2SF;
  }
  fill(255);
    textSize(55); 
    text(active, 118, 125);
    fill(255);
    textSize(55); 
    text(standby, 538, 125);
}
// --------------- Event -----------------------
public void controlEvent(ControlEvent theEvent) 
{
  println(theEvent.getController().getName());
  
}

// -------------- Button -------------------------
public void VHF1(int theValue) 
{
  println("a button event from VHF1: "+theValue);
  for(int i=0;i<12;i++)
  {
    mode[i] = false;
  }
  mode[0]=true;
}

public void VHF2(int theValue) 
{
  println("a button event from VHF2: "+theValue);
  for(int i=0;i<12;i++)
  {
    mode[i] = false;
  }
  mode[1]=true;
}

public void VHF3(int theValue) 
{
  println("a button event from VHF3: "+theValue);
  for(int i=0;i<12;i++)
  {
    mode[i] = false;
  }
  mode[2]=true;
}

public void HF1(int theValue) 
{
  println("a button event from HF1: "+theValue);
  for(int i=0;i<12;i++)
  {
    mode[i] = false;
  }
  mode[3]=true;
}

public void HF2(int theValue) 
{
  println("a button event from VHF2: "+theValue);
  for(int i=0;i<12;i++)
  {
    mode[i] = false;
  }
  mode[4]=true;
}

public void AM(int theValue) 
{
  println("a button event from AM: "+theValue);
  for(int i=0;i<12;i++)
  {
    mode[i] = false;
  }
  mode[5]=true;
}

public void NAV(int theValue) 
{
  println("a button event from NAV: "+theValue);
  for(int i=0;i<12;i++)
  {
    mode[i] = false;
  }
  mode[6]=true;
}

public void VOR(int theValue) 
{
  println("a button event from VOR: "+theValue);
  if(mode[6])
  {
     for(int i=7;i<12;i++)
     {
       mode[i] = false;
     }
     mode[7] = true;
  }
}

public void ILS(int theValue) 
{
  println("a button event from ILS: "+theValue);
  if(mode[6])
  {
     for(int i=7;i<12;i++)
     {
       mode[i] = false;
     }
     mode[8] = true;
  }
}

public void MLS(int theValue) 
{
  println("a button event from MLS: "+theValue);
  if(mode[6])
  {
     for(int i=7;i<12;i++)
     {
       mode[i] = false;
     }
     mode[9] = true;
  }
}

public void ADF(int theValue) 
{
  println("a button event from ADF: "+theValue);
  if(mode[6])
  {
     for(int i=7;i<12;i++)
     {
       mode[i] = false;
     }
     mode[10] = true;
  }
}

public void BFO(int theValue) 
{
  println("a button event from BFO: "+theValue);
  if(mode[6])
  {
     for(int i=7;i<12;i++)
     {
       mode[i] = false;
     }
     mode[11] = true;
  }
}

public void CHANGE(int theValue) 
{
  println("a button event from change: "+theValue);
  float temp;
  if(mode[0])
  {
    temp = vhf1AF;
    vhf1AF = vhf1SF;
    vhf1SF = temp;
  }
  else if(mode[1])
  {
    temp = vhf2AF;
    vhf2AF = vhf2SF;
    vhf2SF = temp;
  }
  else if(mode[2])
  {
    temp = vhf3AF;
    vhf3AF = vhf3SF;
    vhf3SF = temp;
  }
  else if(mode[3])
  {
    temp = hf1AF;
    hf1AF = hf1SF;
    hf1SF = temp;
  }
  else if(mode[4])
  {
    temp = hf2AF;
    hf2AF = hf2SF;
    hf2SF = temp;
  }
}

public void MOINS1(int theValue)
{
   println("a button event from change: "+theValue);
   if(mode[0])
  {
   if(vhf1SF<=118.999)
   {
     vhf1SF += 18;
   }
   else
   {
   vhf1SF -= 1;
   }
  }
  else if(mode[1])
  {
   if(vhf2SF<=118.999)
   {
     vhf2SF += 18;
   }
   else
   {
   vhf2SF -= 1;
   }
  }
  else if(mode[2])
  {
    if(vhf3SF<=118.999)
     {
     vhf3SF += 18;
     }
    vhf3SF -= 1;
  }
  else if(mode[3])
  {
    hf1SF -= 1;
  }
  else if(mode[4])
  {
    hf2SF -= 1;
  }
   
}

public void PLUS1(int theValue)
{
  println("a button event from change: "+theValue);
  if(mode[0])
  {
   if(vhf1SF>=136.000)
   {
     vhf1SF -= 18.000;
   }
   else
   {
   vhf1SF += 1;
   }
  }
  else if(mode[1])
  {
   if(vhf2SF>=136.000)
   {
     vhf2SF -= 18.000;
   }
   else
   {
   vhf2SF += 1;
   }
  }
  else if(mode[2])
  {
    if(vhf3SF>=136.000)
     {
     vhf3SF -= 18.000;
     }
    vhf3SF += 1;
  }
  else if(mode[3])
  {
    hf1SF += 1;
  }
  else if(mode[4])
  {
    hf2SF += 1;
  }
}

public void MOINS2(int theValue)
{
  println("a button event from change: "+theValue);
   if(mode[0])
  {
   if(vhf1SF<=118.000)
   {
   vhf1SF=136.975;  
   }
   else
   {
   vhf1SF -= 0.025;
   }
  }
  else if(mode[1])
  {
   if(vhf2SF<=118.000)
   {
   vhf2SF=136.975;  
   }
   else
   {
   vhf2SF -= 0.025;
   }
  }
  else if(mode[2])
  {
   if(vhf3SF<=118.000)
   {
   vhf3SF=136.975;  
   }
   else
   {
    vhf3SF -= 0.025;
   }
  }
  else if(mode[3])
  {
    hf1SF -= 0.025;
  }
  else if(mode[4])
  {
    hf2SF -= 0.025;
  }
}

public void PLUS2(int theValue)
{
  println("a button event from change: "+theValue);
  if(mode[0])
  {
   if(vhf1SF>=136.975)
   {
     vhf1SF = 118.000;
   }
   else
   {
   vhf1SF += 0.025;
   }
  }
  else if(mode[1])
  {
   if(vhf2SF>=136.975)
   {
     vhf2SF = 118.000;
   }
   else
   {
   vhf2SF += 0.025;
   }
  }
  else if(mode[2])
  {
   if(vhf3SF>=136.975)
   {
     vhf3SF = 118.000;
   }
   else
   {
    vhf3SF += 0.025;
   }
  }
  else if(mode[3])
  {
    hf1SF += 0.025;
  }
  else if(mode[4])
  {
    hf2SF += 0.025;
  }
}
```
