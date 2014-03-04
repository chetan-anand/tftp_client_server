/* All of the following deals with command line switches */
  while ((opt = getopt (argc, argv, "dnoh:P:p:g:l:w:")) != -1)	/* this function is handy */
    {
      switch (opt)
	{
	case 'd':		/* debug mode (no opts) */
	  debug = 1;
	  break;
	case 'P':		/* Port (opt required) */
	  port = atoi (optarg);
	  if (debug)
	    {
	      printf ("Client: The port number is: %d\n", port);
	    }
	  break;
	case 'p':		/* put a file on the server */
	  strncpy (filename, optarg, sizeof (filename) - 1);
	  opcode = WRQ;
	  fp = fopen (filename, "r");	/*opened the file for reading */
	  if (fp == NULL)
	    {
	      printf ("Client: file could not be opened\n");
	      return 0;
	    }
	  if (debug)
	    {
	      printf ("Client: The file name is: %s and can be read",
		      filename);
	    }
	  fclose (fp);
	  break;
	case 'g':		/*get a file from the server */
	  strncpy (filename, optarg, sizeof (filename) - 1);
	  opcode = RRQ;
	  fp = fopen (filename, "w");	/*opened the file for writting */
	  if (fp == NULL)
	    {
	      printf ("Client: file could not be created\n");
	      return 0;
	    }
	  if (debug)
	    {
	      printf ("Client: The file name is: %s and it has been created",
		      filename);
	    }
	  fclose (fp);
	  break;
	case 'w':		/* Get the window size */
	  ackfreq = atoi (optarg);
	  if (debug)
	    {
	      printf ("Client: Window size is: %i\n", ackfreq);
	    }
	  //ackfreq = atoi (optarg);
	  if (ackfreq > MAXACKFREQ)
	    {
	      printf
		("Client: Sorry, you specified an ack frequency higher than the maximum allowed (Requested: %d Max: %d)\n",
		 ackfreq, MAXACKFREQ);
	      return 0;
	    }
	  else if (w_size == 0)
	    {
	      printf ("Client: Sorry, you have to ack sometime.\n");
	      return 0;
	    }
	  break;
	case 'l':		/* packet length */
	  datasize = atoi (optarg);
	  if (debug)
	    {
	      printf ("Client: Packet length is: %i bytes\n", datasize);
	    }
	  if (datasize > MAXDATASIZE)
	    {
	      printf
		("Client: Sorry, you specified a data size higher than the maximum allowed (Requested: %d Max: %d)\n",
		 datasize, MAXDATASIZE);
	      return 0;
	    }
	  break;
	case 'h':		/* Help (no opts) */
	  help (argv[0]);
	  return (0);
	  break;
	case 'o':
	  strncpy (mode, "octet", sizeof (mode) - 1);
	  if (debug)
	    {
	      printf ("Client: The mode is set to octet\n");
	    }
	  break;
	case 'n':
	  strncpy (mode, "netascii", sizeof (mode) - 1);
	  if (debug)
	    {
	      printf ("Client: The mode is set to netascii\n");
	    }
	  break;
	default:		/* everything else */
	  help (argv[0]);
	  return (0);
	  break;
	}			//end of switch
    }				//end of while loop

/*check for valid input*/
  if (argc < 5 || argc > 12)
    {
      printf ("Client: wrong number of arguments: %d\n", argc);
      help (argv[0]);
      exit (ERROR);
    }

/* Done dealing with switches and the command line*/



///////////////////////////////////////////////////////////////////////////////////////////////
