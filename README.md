# Docker-Stats-Go 


Package docker-stats-go provides the ability to get currently running Docker
container statistics, including memory and CPU usage.

To get the statistics of running Docker containers, you can use the `Current()`
function:

    stats, err := dsg.Current()
    if err != nil {
    	panic(err)
    }

    for _, s := range stats {
    	fmt.Println(s.Container) // 9f2656020722
    	fmt.Println(s.Memory) // {Raw=221.7 MiB / 7.787 GiB, Percent=2.78%}
    	fmt.Println(s.CPU) // 99.79%
    }

Alternatively, you can use the `NewMonitor()` function to receive a constant
stream of Docker container stats, available on the Monitor's `Stream` channel:

    m := dsg.NewMonitor()

    for res := range m.Stream {
    	if res.Error != nil {
    		panic(err)
    	}

    	for _, s := range res.Stats {
    		fmt.Println(s.Container) // 9f2656020722
    	}
    }

