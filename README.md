# self-driving-vehicles-graphs
Here is the code to plot graph using the data from self-driving vehicles in different scenarios.

import matplotlib.pyplot as plt
import pandas as pd

df = pd.read_csv('vehicle_tracks_000.csv') #write the csv file name

track_id = df['track_id']
frame_id = df['frame_id']
timestamp_ms = df['timestamp_ms']
agent_type = df['agent_type']
x = df['x']
y = df['y']
vx = df['vx']
vy = df['vy']
psi_rad = df['psi_rad']
length = df['length']
width = df['width']

i=0
j=1
ax = []
ay = []
x_selected = []
y_selected = []
vx_selected = []
vy_selected = []
yaw_rate = []
while j < len(track_id):
    if track_id[j] == track_id[i]:
        ax.append((vx[j]-vx[i])/100)
        ay.append((vy[j]-vy[i])/100)
        yaw_rate.append((psi_rad[j]-psi_rad[i])/100)
    if track_id[i] == 5:                #write track_id number that shows the relationship between vx and vy, x and y
        vx_selected.append(vx[i])
        vy_selected.append(vy[i])
        x_selected.append(x[i])
        y_selected.append(y[i])
    i += 1
    j += 1

fig, axs = plt.subplots(2,6,figsize=(9,3))
axs[0][0].hist(x, bins = 15, edgecolor ='black')
axs[0][1].hist(y, bins = 15, edgecolor ='black')
axs[0][2].hist(vx, bins = 15, edgecolor ='black')
axs[0][3].hist(vy, bins = 15, edgecolor ='black')
axs[0][4].hist(ax, bins = 15, edgecolor ='black')
axs[0][5].hist(ay, bins = 15, edgecolor ='black')
axs[1][0].hist(psi_rad, bins = 15, edgecolor ='black')
axs[1][1].hist(yaw_rate, bins = 100, edgecolor ='black')
axs[1][2].plot(x_selected,y_selected)
axs[1][3].plot(vx_selected,vy_selected)
axs[0][0].set_xlabel('x')
axs[0][1].set_xlabel('y')
axs[0][2].set_xlabel('vx')
axs[0][3].set_xlabel('vy')
axs[0][4].set_xlabel('ax')
axs[0][5].set_xlabel('ay')
axs[1][0].set_xlabel('psi_rad')
axs[1][1].set_xlabel('yaw_rate')
axs[1][2].set_xlabel('relationship between x and y')
axs[1][3].set_xlabel('relationship between vx and vy')
fig.suptitle('Graphs')
plt.show()
