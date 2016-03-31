    # QMES_Code
    #Analysing River Data

    import numpy as np 
    import matplotlib.pyplot as plt
    from scipy import stats

    # Set font size of figures

    plt.rcParams['font.size'] = 9
    plt.tick_params(pad=10)

    # Load textfiles from their folder

    RiverData1 = np.loadtxt('Gray1961.txt', skiprows = 2)
    RiverData2 = np.loadtxt('Hack1957.txt', skiprows = 2)
    RiverData3 = np.loadtxt('Rignon1996.txt', skiprows = 2)
    RiverData4 = np.loadtxt('Robert1990.txt', skiprows = 2)
    RiverData5 = np.loadtxt('Langbein1947_p145.txt', skiprows = 2)
    RiverData6 = np.loadtxt('Langbein1947_p146.txt', skiprows = 2)
    RiverData7 = np.loadtxt('Langbein1947_p149.txt', skiprows = 2)
    RiverData8 = np.loadtxt('Langbein1947_p152.txt', skiprows = 2)

    # Assign RiverData's to a list
    # Total the num of variables in the list
    # create a loop assigning i to each River_Data Variable

    plotnum = 1
    River_list = [RiverData1,RiverData2,RiverData3,RiverData4,RiverData5,RiverData6,RiverData7,RiverData8]
    River_list_len=len(River_list)
    for i in range(0,River_list_len):           
        plt.subplot(2,4,plotnum)
        plt.plot((River_list[i][:,0]),(River_list[i][:,1]),'ko')
        m,c,_,_,_ = stats.linregress(np.log(River_list[i][:,0]),np.log(River_list[i][:,1]))
        m1 = round(m,2)
        c1 = round(c,2)
        # ranges our x values together #    
        xfit = np.arange(0.1,400,0.1)
        # equation of a straight line #
        yfit = np.exp(c)*xfit**m
        plt.plot(xfit, yfit, label = 'Best Fit')
        #plt.legend(x, y, eqn)
        eqn = 'y = ' + (str(xfit**m)) + 'x + ' + (str(np.exp(c)))   
        plt.xlabel('Area (Km$^2$)')
        plt.ylabel('River Length (km)') 
        plt.xscale('log')
        plt.yscale('log')       
        plt.legend('Data', 'Line of Best Fit', loc ='upper left')
        plt.text(10,1,eqn) 
        plotnum= plotnum++1


    plt.show()
