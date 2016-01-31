package se.lab4;

/**
 * This class is responsible for maintaining valid meeting object.<BR>
 * By saying valid means both start and stop {@link CTime} objects should be valid, also, stop time
 * always after the start time and that no meeting lasts more than 1 hour.<BR>
 * Also, location is important in TimeZone decision.
 *
 * @author Rugal Bernstein
 */
public class CMeeting implements Comparable<CMeeting>, Cloneable
{

    private static final String OUTPUT_TEMPLATE = "CMeeting\n  start=%s\n  stop=%s\n  location=%s";

    private static final TimeZone DEFAULT_TIMEZONE = TimeZone.Toronto;

    private final CTime start;

    private final CTime stop;

    private final TimeZone location;

    /**
     * Internal used for replication only.
     *
     * @param start
     * @param stop
     * @param location
     */
    private CMeeting(CTime start, CTime stop, TimeZone location)
    {
        this.start = start;
        this.stop = stop;
        this.location = location;
    }

    /**
     * Initialize object with default time zone
     *
     * @param startHour
     * @param startMinute
     * @param stopHour
     * @param stopMinute
     */
    public CMeeting(int startHour, int startMinute, int stopHour, int stopMinute)
    {
        this(startHour, startMinute, stopHour, stopMinute, DEFAULT_TIMEZONE);
    }

    /**
     * Initialize object with all parameters specified. Start and stop time should be valid, which
     * means CTime object and meeting time duration should valid.
     *
     * @param startHour
     * @param startMinute
     * @param stopHour
     * @param stopMinute
     * @param location
     *
     * @throws IllegalArgumentException will be thrown when illegal start and stop time specified.
     */
    public CMeeting(int startHour, int startMinute, int stopHour, int stopMinute, TimeZone location)
    {
        this.location = location;
        CTime newStart = new CTime(startHour, startMinute, location.getTimeZone());
        CTime newStop = new CTime(stopHour, stopMinute, location.getTimeZone());
        int duration = newStop.compareTo(newStart);
        if (!isValidMeeting(duration))
        {
            throw new IllegalArgumentException();
        }
        this.start = newStart;
        this.stop = newStop;
    }

    private boolean isValidMeeting(int duration)
    {
        return duration > 0 && duration <= 60;
    }

    /**
     * Get new instance that the content of it is the same as start object.
     *
     * @return
     */
    public CTime getStart()
    {
        CTime time = null;
        try
        {
            time = start.clone();
        }
        catch (CloneNotSupportedException ex)
        {

        }
        return time;
    }

    /**
     * Get new instance that the content of it is the same as stop object.
     *
     * @return
     */
    public CTime getStop()
    {
        CTime time = null;
        try
        {
            time = stop.clone();
        }
        catch (CloneNotSupportedException ex)
        {

        }
        return time;
    }

    public TimeZone getLocation()
    {
        return location;
    }

    @Override
    public String toString()
    {
        return String.format(OUTPUT_TEMPLATE, start, stop, location.name());
    }

    /**
     *
     * This method used for comparing if 2 meetings are conflicting.<BR>
     *
     * @param other
     *
     * @return -1 stands for current object is earlier than the other; 1 stands for reversed
     *         situation. 0 stands for somehow overlapping happens.
     */
    @Override
    public int compareTo(CMeeting other)
    {
        if (this.stop.compareTo(other.start) <= 0)
        {
            return -1;
        }
        if (other.stop.compareTo(this.start) <= 0)
        {
            return 1;
        }
        return 0;
    }

    /**
     * Replicate a CMeeting object for preventing external reference.
     *
     * @return
     *
     * @throws java.lang.CloneNotSupportedException
     *
     *
     */
    @Override
    protected CMeeting clone() throws CloneNotSupportedException
    {
        return (CMeeting) super.clone();
    }
}
