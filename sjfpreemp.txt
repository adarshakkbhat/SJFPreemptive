#include<stdio.h>
int main()
{
    int n,at[10],bt[10],ct[10],i,minat,total=0,count=0,minbt,temp[10],pos,minbt1,minat1;
    printf("Enter the number of processes\n");
    scanf("%d",&n);
    printf("AT    BT\n");
    for(i=0;i<n;i++)
    {
        scanf("%d %d",&at[i],&bt[i]);
        temp[i]=bt[i];
    }
    minat=at[0];//initialize first at to minat
    for(i=0;i<n;i++)
    {
        if(at[i]<minat)//checking for small at
        minat=at[i];
    }
    total=minat;//initialize total with minat
    while(count!=n)
    {
        minbt=999;
        for(i=0;i<n;i++)
        {
            if(at[i]<=minat)//checking the process came within minat
            {
                if(bt[i]<minbt)//checking for small bt
                {
                    minbt=bt[i];
                    pos=i;//saving the position
                }
            }
        }
        if(minbt==999)//haven't found any process within minat(all at's are greater than minat)
        { //we have to find minimum of at's which are greater than minat
          minbt1=999;//To exclude completed processes
          minat1=999;
          for(i=0;i<n;i++)
          {
              if(bt[i]<minbt1)//not a completed process
              {               //checking at[i]>minat is useless because it would have detected earlier if it is less than minat
                  if(at[i]<minat1)//finding small at
                     minat1=at[i];
              }
           }
           total=total+minat1-minat;//Add idle time to total
           minat=minat1;//new minat
           printf("minat1 %d\n",minat);  
        }
        else
        {
        bt[pos]--;
        total++;
        minat=total;
        if(bt[pos]==0)
        {
            count++;
            ct[pos]=total;
            bt[pos]=999;
        }
        }
    }
    printf("P\t\tAT\t\tBT\t\tCT\t\tTAT\t\tWT\n");
    for(i=0;i<n;i++)
    {
        printf("%d\t\t%d\t\t%d\t\t%d\t\t%d\t\t%d\n",i+1,at[i],temp[i],ct[i],ct[i]-at[i],ct[i]-at[i]-temp[i]);
    }
}