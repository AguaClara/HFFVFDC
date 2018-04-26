```python
from aide_design.play import*
from aide_design.physchem import*
Q_Plant=1*u.L/u.s
Temp_Plant=20*u.degC
RatioVCOrifice=.62
Nu=viscosity_kinematic(Temp_Plant)
print(Nu)
Max_Num_Holes=19
Q_Per_Hole=Q_Plant/Max_Num_Holes
print(Q_Per_Hole)
#Rows_Per_T_Active_Area= 1 or 2
#Active_Height_Of_T=.13*u.m
#Min/Max_Orifices_Per_Row=
Avail_Head_High_Est=2*u.m
Avail_Head_Low_Est=1*u.m

Outlet_Diam=2*u.inch
Area_Outlet=((Outlet_Diam/2)**2)*u.pi/4
Slider_Pipe_ID=1.5*u.inch
SliderPipeLength=.405*u.m
Slider_Hole_Diam=.25*u.inch
Area_Slider_Hole=(((Slider_Hole_Diam/2)**2)*u.pi/4)
print(Area_Slider_Hole.to(u.m**2))
V_Outlet=Q_Plant/((Outlet_Diam/2)**2)*u.pi/4
print(V_Outlet.to(u.m/u.s))

V_Hole=(Q_Per_Hole/Area_Slider_Hole)
print(V_Hole.to(u.m/u.s))
Reynolds=re_pipe(Q_Per_Hole, Slider_Hole_Diam, Nu)
print(Reynolds)
overall_length=40.5 *u.cm
tee_height=5.25*u.inch  
bushing_lip=.21875*u.inch   
bushing_height=1*u.inch   
tee_exposed=tee_height-2*bushing_height+bushing_lip
top_space=1.75*u.inch
bottom_space=bushing_height+tee_exposed+Slider_Hole_Diam/2
L_active=overall_length-top_space-bottom_space
print(L_active)
hole_rows=7
rows_exposed=3
row_spacing=tee_exposed/rows_exposed

HL_Inlet=headloss_exp(Q_Plant, Outlet_Diam, K_Minor_Inlet)
print(HL_Inlet)

HL_Slider_Hole=head_orifice(Slider_Hole_Diam, RatioVCOrifice, Q_Per_Hole)
print(HL_Slider_Hole)


flow_orifice_1= flow_orifice(Slider_Hole_Diam, 1*u.m, RatioVCOrifice).to(u.L/u.s)
print(90*flow_orifice_1)##Given 1 meter of head, slider pipe diam can handle an excess of 7 L/s which is more than what the 2 inch tee can handle, 6.4 L/s
Two_inch_HFFV_Max_Holes=(6*u.L/u.s)/flow_orifice_1 ##69 holes
flow_orifice_2= flow_orifice(Slider_Hole_Diam, 2*u.m, RatioVCOrifice)
print(flow_orifice_2.to(u.L/u.s))


##End headloss and general parameters
```

```python
##Float ideas
from aide_design.play import*
from aide_design.physchem import*
import math
Temp_Plant=20*u.degC
Weight_Slider_Pipe=.3192*u.kg


Float_ID=1*u.inch   
Area_Float=Float_ID**2*math.pi
Float_OD=3.47*u.cm  
print((Float_OD/2).to(u.inch))
Spacing=2*u.cm
print(Float_ID+Spacing)
print((Float_OD+Spacing).to(u.inch))
print(2.154-1.787)
Area=(3*Float_OD+2*Spacing)*Float_OD
print(Area.to(u.m**2))

##Spring test  
Delta_X=45.93*u.mm   
Mass=1.0763*u.kg
W=Mass*u.gravity
k=W/Delta_X
print(k.to(u.N/u.m))
print(W.to(u.N))
Static_Friction_Force=17.67*u.N   
Original_Length=33.13*u.mm
New_Length=110*u.mm   
Delta_X2=76.87*u.mm  
F=Delta_X2*k
print(F.to(u.N))

Mass_Float=(F/u.gravity).to(u.kg)
print(Mass_Float)

Volume_Float_Spring=Mass_Float/density_water(Temp_Plant)
L_Float_Spring=Volume_Float_Spring/Area_Float
print(L_Float_Spring.to(u.inch))

import math
##What friction force does the smaller float's buoyant force support?
Smol_Float_ID=.5*u.inch
Area_Smol_Float=Smol_Float_ID**2*math.pi
Volume_Smol_Float=3*Area_Smol_Float*L_Float_Spring
Mass_Smol_Float=Volume_Smol_Float*density_water(Temp_Plant)
F_Smol_Float=(Mass_Smol_Float*u.gravity).to(u.N)
print(F_Smol_Float)


```
```python
def K_Minor_Calc(D1,D2):
  K_L=(1-D1**2/D2**2)**2
  return(K_L)
V=(1*u.m*9.81*u.m/u.s**2)**.5
print(V)
A=((1*u.inch)**2)/4*math.pi
Q=V*A
Q.to(u.L/u.s)
#In this system we are bottlenecked by our 1 inch piping but in real plants it will be bottlenecked by the tee as the piping going into the tee will be the same pipe sizing.
#Headloss calculation in experimental setup
Q_HFFV=1*u.L/u.s  
Pipe_Roughness=0.0015*u.mm
Pipe_in=1*u.inch   
Pipe_Tee=2*u.inch  
Length_Sys=6*u.inch
K_adapter=K_Minor_Calc(Pipe_in,Pipe_Tee)
K_elbows=.5*2
K=K_adapter+K_elbows
headloss_exp(Q_HFFV,Pipe_Tee,K)
headloss_fric(Q_HFFV, Pipe_Tee, Length_Sys, Nu,Pipe_Roughness)
```
