# Dimensions Control

Elementor dimensions control displays a input fields for top, right, bottom, left and the option to link them together.

The control is defined in `Control_Dimensions` class which extends `Control_Base_Units` class.

Note that when using the control, the type should be set using the `\Elementor\Controls_Manager::DIMENSIONS` constant.

## Arguments

<table>
	<thead>
		<tr>
			<th>Name</th>
			<th>Type</th>
			<th>Default</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td><code>type</code></td>
			<td><code>string</code></td>
			<td>slider</td>
			<td>The type of the control.</td>
		</tr>
		<tr>
			<td><code>label</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>The label that appears above of the field.</td>
		</tr>
		<tr>
			<td><code>description</code></td>
			<td><code>string</code></td>
			<td></td>
			<td>The description that appears below the field.</td>
		</tr>
		<tr>
			<td><code>show_label</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>Whether to display the label.</td>
		</tr>
		<tr>
			<td><code>label_block</code></td>
			<td><code>bool</code></td>
			<td>true</td>
			<td>Whether to display the label in a separate line.</td>
		</tr>
		<tr>
			<td><code>separator</code></td>
			<td><code>string</code></td>
			<td>default</td>
			<td>Set the position of the control separator. Available values are <code>default</code>, <code>before</code>, <code>after</code> and <code>none</code>. <code>default</code> will position the separator depending on the control type. <code>before</code> / <code>after</code> will position the separator before/after the control. <code>none</code> will hide the separator.</td>
		</tr>
		<tr>
			<td><code>size_units</code></td>
			<td><code>array</code></td>
			<td>[ ‘px’ ]</td>
			<td>An array of available CSS units like <code>px</code>, <code>em</code>, <code>rem</code>, <code>%</code>, <code>deg</code> and <code>vh</code>.</td>
		</tr>
		<tr>
			<td><code>range</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				An array of ranges for each register size.
				<p></p>
				<ul>
					<li><strong>$min</strong> (<code>int</code>) The minimum value of range.</li>
					<li><strong>$max</strong> (<code>int</code>) The maximum value of range.</li>
					<li><strong>$step</strong> (<code>int</code>) The intervals value that will be incremented or decremented when using the controls’ spinners.</li>
				</ul>
			</td>
		</tr>
		<tr>
			<td><code>default</code></td>
			<td><code>array</code></td>
			<td></td>
			<td>
				Default slider value.
				<p></p>
				<ul>
					<li><strong>$unit</strong> (<code>string</code>) Initial unit of the slider.</li>
					<li><strong>$size</strong> (<code>int</code>) Initial size of the slider.</li>
				</ul>
			</td>
		</tr>
	</tbody>
</table>

## Return Value

```
[
	'top' => '',
	'right' => '',
	'bottom' => '',
	'left' => '',
	'unit' => '',
	'isLinked' => '',
]
```

(_`array`_) An array containing the dimension values:

* **$top** (_`int`_) Top dimension.
* **$right** (_`int`_) Right dimension.
* **$bottom** (_`int`_) Bottom dimension.
* **$left** (_`int`_) Left dimension.
* **$unit** (_`string`_) The CSS unit type.
* **$isLinked** (_`bool`_) Whether to link all the values together or not.

## Usage

```php {14-24,32,37}
<?php
class Elementor_Test_Widget extends \Elementor\Widget_Base {

	protected function _register_controls() {

		$this->start_controls_section(
			'content_section',
			[
				'label' => __( 'Content', 'plugin-name' ),
				'tab' => \Elementor\Controls_Manager::TAB_CONTENT,
			]
		);

		$this->add_control(
			'margin',
			[
				'label' => __( 'Margin', 'plugin-name' ),
				'type' => Controls_Manager::DIMENSIONS,
				'size_units' => [ 'px', '%', 'em' ],
				'selectors' => [
					'{{WRAPPER}} .your-class' => 'margin: {{TOP}}{{UNIT}} {{RIGHT}}{{UNIT}} {{BOTTOM}}{{UNIT}} {{LEFT}}{{UNIT}};',
				],
			]
		);

		$this->end_controls_section();

	}

	protected function render() {
		$settings = $this->get_settings_for_display();
		echo '<div class="your-class"> ... </div>';
	}

	protected function _content_template() {
		?>
		<div class="your-class"> ... </div>
		<?php
	}

}
```