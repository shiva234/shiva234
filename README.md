### Hi there 👋

<!--
**shiva234/shiva234** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub pro.
my name is shiva jee.i am building a meditation app name angel help people to meditate anywhere on the planet.
i am using google technologies:google earth engine,google map platforms,kotlin ,angular.
i am  passionate about to bring change in people life.
here is code of my app, some basic 
import android.os.Bundle
import android.os.CountDownTimer
import androidx.appcompat.app.AppCompatActivity
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    private lateinit var timer: CountDownTimer

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        startButton.setOnClickListener {
            val timeInMinutes = timeEditText.text.toString().toLong()
            val timeInMillis = timeInMinutes * 60 * 1000

            timer = object : CountDownTimer(timeInMillis, 1000) {
                override fun onTick(millisUntilFinished: Long) {
                    val minutesLeft = millisUntilFinished / 1000 / 60
                    val secondsLeft = millisUntilFinished / 1000 % 60
                    timerTextView.text = "$minutesLeft:${String.format("%02d", secondsLeft)}"
                }

                override fun onFinish() {
                    timerTextView.text = "Meditation finished"
                }
            }

            timer.start()
        }

        stopButton.setOnClickListener {
            if (::timer.isInitialized) {
                timer.cancel()
                timerTextView.text = "Meditation stopped"
            }
        }
    }
implementation 'com.google.android.gms:play-services-maps:18.0.1'
<com.google.android.gms.maps.MapView
    android:id="@+id/mapView"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import com.google.android.gms.maps.GoogleMap
import com.google.android.gms.maps.MapView
import com.google.android.gms.maps.OnMapReadyCallback
import com.google.android.gms.maps.model.LatLng
import com.google.android.gms.maps.model.MarkerOptions

class MainActivity : AppCompatActivity(), OnMapReadyCallback {

    private lateinit var mapView: MapView
    private lateinit var googleMap: GoogleMap

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        mapView = findViewById(R.id.mapView)
        mapView.onCreate(savedInstanceState)
        mapView.getMapAsync(this)
    }

    override fun onMapReady(map: GoogleMap?) {
        map?.let {
            googleMap = it
            val sydney = LatLng(-34.0, 151.0)
            googleMap.addMarker(MarkerOptions().position(sydney).title("Marker in Sydney"))
            googleMap.moveCamera(CameraUpdateFactory.newLatLng(sydney))
        }
    }

    override fun onResume() {
        super.onResume()
        mapView.onResume()
    }

    override fun onPause() {
        super.onPause()
        mapView.onPause()
    }

    override fun onDestroy() {
        super.onDestroy()
        mapView.onDestroy()
    }

    override fun onLowMemory() {
        super.onLowMemory()
        mapView.onLowMemory()
    }
}

